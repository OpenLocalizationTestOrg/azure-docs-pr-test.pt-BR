---
title: "Tutorial: Integração do Azure Active Directory ao Canvas LMS | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Canvas LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 8f4a09266a108e2c92326b0909dd0650b1c84d6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="aa4a9-103">Tutorial: Integração do Azure Active Directory ao Canvas LMS</span><span class="sxs-lookup"><span data-stu-id="aa4a9-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="aa4a9-104">Neste tutorial, você aprenderá como toointegrate tela com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="aa4a9-104">In this tutorial, you learn how toointegrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="aa4a9-105">Tela de integrar o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-105">Integrating Canvas with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="aa4a9-106">Você pode controlar no AD do Azure que tenha acesso tooCanvas</span><span class="sxs-lookup"><span data-stu-id="aa4a9-106">You can control in Azure AD who has access tooCanvas</span></span>
- <span data-ttu-id="aa4a9-107">Você pode habilitar seus usuários tooautomatically get conectado tooCanvas (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-107">You can enable your users tooautomatically get signed-on tooCanvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="aa4a9-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="aa4a9-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="aa4a9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa4a9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aa4a9-110">Prerequisites</span></span>

<span data-ttu-id="aa4a9-111">tooconfigure integração do AD do Azure com o Canvas, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-111">tooconfigure Azure AD integration with Canvas, you need hello following items:</span></span>

- <span data-ttu-id="aa4a9-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="aa4a9-113">Uma assinatura habilitada para logon único do Canvas</span><span class="sxs-lookup"><span data-stu-id="aa4a9-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="aa4a9-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="aa4a9-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="aa4a9-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="aa4a9-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="aa4a9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="aa4a9-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="aa4a9-118">Scenario description</span></span>
<span data-ttu-id="aa4a9-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="aa4a9-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="aa4a9-121">Tela Adicionar da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="aa4a9-121">Adding Canvas from hello gallery</span></span>
2. <span data-ttu-id="aa4a9-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-hello-gallery"></a><span data-ttu-id="aa4a9-123">Tela Adicionar da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="aa4a9-123">Adding Canvas from hello gallery</span></span>
<span data-ttu-id="aa4a9-124">integração de saudação tooconfigure da tela no AD do Azure, você precisa tooadd tela da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-124">tooconfigure hello integration of Canvas into Azure AD, you need tooadd Canvas from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="aa4a9-125">**tooadd tela da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="aa4a9-125">**tooadd Canvas from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa4a9-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="aa4a9-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="aa4a9-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="aa4a9-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="aa4a9-133">Na caixa de pesquisa hello, digite **tela**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-133">In hello search box, type **Canvas**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="aa4a9-135">No painel de resultados de saudação, selecione **tela**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-135">In hello results panel, select **Canvas**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="aa4a9-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="aa4a9-138">Nesta seção, você configura e testa o logon único do Azure AD com o Canvas, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="aa4a9-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na tela é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Canvas is tooa user in Azure AD.</span></span> <span data-ttu-id="aa4a9-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário de saudação relacionado na tela precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-140">In other words, a link relationship between an Azure AD user and hello related user in Canvas needs toobe established.</span></span>

<span data-ttu-id="aa4a9-141">Na tela, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-141">In Canvas, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="aa4a9-142">tooconfigure e teste com tela de logon único do AD do Azure, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-142">tooconfigure and test Azure AD single sign-on with Canvas, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="aa4a9-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="aa4a9-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="aa4a9-145">**[Criar um usuário de teste de tela](#creating-a-canvas-test-user)**  -toohave um equivalente do Britta Simon na tela que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - toohave a counterpart of Britta Simon in Canvas that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="aa4a9-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="aa4a9-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="aa4a9-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="aa4a9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="aa4a9-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de tela.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="aa4a9-150">**tooconfigure AD do Azure-logon único com o Canvas, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="aa4a9-150">**tooconfigure Azure AD single sign-on with Canvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa4a9-151">Em Olá portal do Azure, Olá **tela** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-151">In hello Azure portal, on hello **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="aa4a9-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="aa4a9-155">Em Olá **domínio da tela e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-155">On hello **Canvas Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="aa4a9-157">a.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-157">a.</span></span> <span data-ttu-id="aa4a9-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="aa4a9-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="aa4a9-159">b.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-159">b.</span></span> <span data-ttu-id="aa4a9-160">Em Olá **identificador** texto, o valor do tipo hello usando saudação padrão a seguir:`https://<tenant-name>.instructure.com/saml2`</span><span class="sxs-lookup"><span data-stu-id="aa4a9-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="aa4a9-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-161">These values are not real.</span></span> <span data-ttu-id="aa4a9-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="aa4a9-163">Entre em contato com [equipe de suporte do cliente de tela](https://community.canvaslms.com/community/help) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) tooget these values.</span></span> 
 
4. <span data-ttu-id="aa4a9-164">Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** o valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="aa4a9-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="aa4a9-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="aa4a9-168">Em Olá **tela configuração** seção, clique em **tela Configurar** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-168">On hello **Canvas Configuration** section, click **Configure Canvas** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="aa4a9-169">Saudação de cópia **alterar a URL da senha, URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="aa4a9-169">Copy hello **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="aa4a9-171">Em uma janela de navegador web diferente, faça logon no site da empresa tooyour tela como um administrador.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-171">In a different web browser window, log in tooyour Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="aa4a9-172">Vá muito**cursos \> contas gerenciadas \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-172">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="aa4a9-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="aa4a9-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="aa4a9-174">No painel de navegação Olá Olá esquerda, selecione **autenticação**e, em seguida, clique em **adicionar nova configuração de SAML**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-174">In hello navigation pane on hello left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="aa4a9-175">![Autenticação](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Autenticação")</span><span class="sxs-lookup"><span data-stu-id="aa4a9-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="aa4a9-176">Na página de integração atual hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-176">On hello Current Integration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="aa4a9-177">![Integração Atual](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "integração Atual")</span><span class="sxs-lookup"><span data-stu-id="aa4a9-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="aa4a9-178">a.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-178">a.</span></span> <span data-ttu-id="aa4a9-179">Em **ID da entidade IdP** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-179">In **IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="aa4a9-180">b.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-180">b.</span></span> <span data-ttu-id="aa4a9-181">Em **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-181">In **Log On URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="aa4a9-182">c.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-182">c.</span></span> <span data-ttu-id="aa4a9-183">Em **URL de logoff** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-183">In **Log Out URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="aa4a9-184">d.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-184">d.</span></span> <span data-ttu-id="aa4a9-185">Em **alterar Link de senha** caixa de texto valor Olá colar **alterar a URL da senha** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-185">In **Change Password Link** textbox, paste hello value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="aa4a9-186">e.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-186">e.</span></span> <span data-ttu-id="aa4a9-187">Em **impressão digital do certificado** caixa de texto, colar Olá **impressão digital** o valor de certificado que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-187">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="aa4a9-188">f.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-188">f.</span></span> <span data-ttu-id="aa4a9-189">De saudação **logon atributo** lista, selecione **NameID**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-189">From hello **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="aa4a9-190">g.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-190">g.</span></span> <span data-ttu-id="aa4a9-191">De saudação **formato do identificador** lista, selecione **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-191">From hello **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="aa4a9-192">h.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-192">h.</span></span> <span data-ttu-id="aa4a9-193">Clique em **Salvar Configurações de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="aa4a9-194">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="aa4a9-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="aa4a9-195">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="aa4a9-196">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="aa4a9-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="aa4a9-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="aa4a9-198">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="aa4a9-200">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="aa4a9-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa4a9-201">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="aa4a9-203">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="aa4a9-205">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="aa4a9-207">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="aa4a9-209">a.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-209">a.</span></span> <span data-ttu-id="aa4a9-210">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="aa4a9-211">b.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-211">b.</span></span> <span data-ttu-id="aa4a9-212">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="aa4a9-213">c.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-213">c.</span></span> <span data-ttu-id="aa4a9-214">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="aa4a9-215">d.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-215">d.</span></span> <span data-ttu-id="aa4a9-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="aa4a9-217">Criando um usuário de teste do Canvas</span><span class="sxs-lookup"><span data-stu-id="aa4a9-217">Creating a Canvas test user</span></span>

<span data-ttu-id="aa4a9-218">tooenable AD do Azure usuários toolog em tooCanvas, eles devem ser provisionados no Canvas.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-218">tooenable Azure AD users toolog in tooCanvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="aa4a9-219">No caso do Canvas, o provisionamento de usuário é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="aa4a9-220">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="aa4a9-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa4a9-221">Faça logon no tooyour **tela** locatário.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-221">Log in tooyour **Canvas** tenant.</span></span>

2. <span data-ttu-id="aa4a9-222">Vá muito**cursos \> contas gerenciadas \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-222">Go too**Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="aa4a9-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="aa4a9-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="aa4a9-224">Clique em **Usuários**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-224">Click **Users**.</span></span>
   
   <span data-ttu-id="aa4a9-225">![Usuários](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="aa4a9-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="aa4a9-226">Clique em **Adicionar Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="aa4a9-227">![Usuários](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="aa4a9-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="aa4a9-228">Em Olá adicionar uma página da caixa de diálogo Novo usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa4a9-228">On hello Add a New User dialog page, perform hello following steps:</span></span>
   
   <span data-ttu-id="aa4a9-229">![Adicionar Usuário](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="aa4a9-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="aa4a9-230">a.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-230">a.</span></span> <span data-ttu-id="aa4a9-231">Em Olá **nome completo** caixa de texto, insira o nome de saudação do usuário, como **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-231">In hello **Full Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="aa4a9-232">b.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-232">b.</span></span> <span data-ttu-id="aa4a9-233">Em Olá **Email** caixa de texto, insira o email de saudação do usuário como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="aa4a9-233">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="aa4a9-234">c.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-234">c.</span></span> <span data-ttu-id="aa4a9-235">Em Olá **Login** caixa de texto, digite o endereço de email do usuário de saudação do AD do Azure como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="aa4a9-235">In hello **Login** textbox, enter hello user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="aa4a9-236">d.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-236">d.</span></span> <span data-ttu-id="aa4a9-237">Selecione **Email que o usuário sobre a criação de conta Olá**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-237">Select **Email hello user about this account creation**.</span></span>

   <span data-ttu-id="aa4a9-238">e.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-238">e.</span></span> <span data-ttu-id="aa4a9-239">Clique em **Adicionar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="aa4a9-240">Você pode usar qualquer outra tela usuário conta ferramenta de criação ou APIs fornecidas pelo Canvas tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-240">You can use any other Canvas user account creation tools or APIs provided by Canvas tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="aa4a9-241">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="aa4a9-242">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCanvas.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCanvas.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="aa4a9-244">**tooassign Britta Simon tooCanvas, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="aa4a9-244">**tooassign Britta Simon tooCanvas, perform hello following steps:**</span></span>

1. <span data-ttu-id="aa4a9-245">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="aa4a9-247">Na lista de aplicativos hello, selecione **tela**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-247">In hello applications list, select **Canvas**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="aa4a9-249">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="aa4a9-251">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-251">Click **Add** button.</span></span> <span data-ttu-id="aa4a9-252">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="aa4a9-254">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="aa4a9-255">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="aa4a9-256">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="aa4a9-257">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="aa4a9-257">Testing single sign-on</span></span>

<span data-ttu-id="aa4a9-258">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="aa4a9-259">Quando você clica em um bloco de tela de Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de tela.</span><span class="sxs-lookup"><span data-stu-id="aa4a9-259">When you click hello Canvas tile in hello Access Panel, you should get automatically signed-on tooyour Canvas application.</span></span>
<span data-ttu-id="aa4a9-260">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="aa4a9-260">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="aa4a9-261">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="aa4a9-261">Additional resources</span></span>

* [<span data-ttu-id="aa4a9-262">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="aa4a9-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="aa4a9-263">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="aa4a9-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

