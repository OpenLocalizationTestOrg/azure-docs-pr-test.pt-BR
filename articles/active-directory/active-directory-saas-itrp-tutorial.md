---
title: "Tutorial: integração do Azure Active Directory com o ITRP | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ITRP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 35463a55fcfc1e55c90700737961c1ff2e58992a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="164b7-103">Tutorial: integração do Azure Active Directory com o ITRP</span><span class="sxs-lookup"><span data-stu-id="164b7-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="164b7-104">Neste tutorial, você aprenderá como toointegrate ITRP com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="164b7-104">In this tutorial, you learn how toointegrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="164b7-105">Integrando o ITRP com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="164b7-105">Integrating ITRP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="164b7-106">Você pode controlar no AD do Azure que tenha acesso tooITRP</span><span class="sxs-lookup"><span data-stu-id="164b7-106">You can control in Azure AD who has access tooITRP</span></span>
- <span data-ttu-id="164b7-107">Você pode habilitar seu usuários tooautomatically get conectado tooITRP (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="164b7-107">You can enable your users tooautomatically get signed-on tooITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="164b7-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="164b7-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="164b7-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="164b7-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="164b7-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="164b7-110">Prerequisites</span></span>

<span data-ttu-id="164b7-111">tooconfigure integração do AD do Azure com ITRP, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="164b7-111">tooconfigure Azure AD integration with ITRP, you need hello following items:</span></span>

- <span data-ttu-id="164b7-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="164b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="164b7-113">Uma assinatura habilitada para logon único do ITRP</span><span class="sxs-lookup"><span data-stu-id="164b7-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="164b7-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="164b7-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="164b7-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="164b7-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="164b7-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="164b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="164b7-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="164b7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="164b7-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="164b7-118">Scenario description</span></span>
<span data-ttu-id="164b7-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="164b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="164b7-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="164b7-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="164b7-121">Adicionando ITRP da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="164b7-121">Adding ITRP from hello gallery</span></span>
2. <span data-ttu-id="164b7-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="164b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-hello-gallery"></a><span data-ttu-id="164b7-123">Adicionando ITRP da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="164b7-123">Adding ITRP from hello gallery</span></span>
<span data-ttu-id="164b7-124">tooconfigure Olá integração do ITRP tooAzure AD, é necessário tooadd ITRP da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="164b7-124">tooconfigure hello integration of ITRP in tooAzure AD, you need tooadd ITRP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="164b7-125">**tooadd ITRP da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="164b7-125">**tooadd ITRP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="164b7-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="164b7-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="164b7-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="164b7-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="164b7-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="164b7-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="164b7-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="164b7-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="164b7-133">Na caixa de pesquisa hello, digite **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="164b7-133">In hello search box, type **ITRP**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="164b7-135">No painel de resultados de saudação, selecione **ITRP**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="164b7-135">In hello results panel, select **ITRP**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="164b7-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="164b7-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="164b7-138">Nesta seção, você configurará e testará o logon único do Azure AD com o ITRP, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="164b7-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="164b7-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no ITRP é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="164b7-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ITRP is tooa user in Azure AD.</span></span> <span data-ttu-id="164b7-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no ITRP precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="164b7-140">In other words, a link relationship between an Azure AD user and hello related user in ITRP needs toobe established.</span></span>

<span data-ttu-id="164b7-141">No ITRP, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="164b7-141">In ITRP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="164b7-142">tooconfigure e teste de logon único do AD do Azure com ITRP, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="164b7-142">tooconfigure and test Azure AD single sign-on with ITRP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="164b7-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="164b7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="164b7-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="164b7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="164b7-145">**[Criando um ITRP testar usuário](#creating-an-itrp-test-user)**  -toohave um equivalente do Britta Simon no ITRP é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="164b7-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - toohave a counterpart of Britta Simon in ITRP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="164b7-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="164b7-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="164b7-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="164b7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="164b7-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="164b7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="164b7-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo ITRP.</span><span class="sxs-lookup"><span data-stu-id="164b7-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="164b7-150">**tooconfigure AD do Azure-logon único com ITRP, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="164b7-150">**tooconfigure Azure AD single sign-on with ITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="164b7-151">Em Olá portal do Azure, Olá **ITRP** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="164b7-151">In hello Azure portal, on hello **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="164b7-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="164b7-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="164b7-155">Em Olá **ITRP domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="164b7-155">On hello **ITRP Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="164b7-157">a.</span><span class="sxs-lookup"><span data-stu-id="164b7-157">a.</span></span> <span data-ttu-id="164b7-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="164b7-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="164b7-159">b.</span><span class="sxs-lookup"><span data-stu-id="164b7-159">b.</span></span> <span data-ttu-id="164b7-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="164b7-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="164b7-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="164b7-161">These values are not real.</span></span> <span data-ttu-id="164b7-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="164b7-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="164b7-163">Entre em contato com [equipe de suporte do cliente ITRP](https://www.itrp.com/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="164b7-163">Contact [ITRP Client support team](https://www.itrp.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="164b7-164">Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** o valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="164b7-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="164b7-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="164b7-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="164b7-168">Em Olá **ITRP configuração** seção, clique em **configurar ITRP** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="164b7-168">On hello **ITRP Configuration** section, click **Configure ITRP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="164b7-169">Saudação de cópia **SAML Single Sign-On URL do serviço e a URL de logout** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="164b7-169">Copy hello **SAML Single Sign-On Service URL and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="164b7-171">Em uma janela de navegador web diferente, faça logon no site da empresa ITRP tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="164b7-171">In a different web browser window, log in tooyour ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="164b7-172">Na barra de ferramentas de saudação na parte superior do hello, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="164b7-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="164b7-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="164b7-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="164b7-174">No painel de navegação esquerdo hello, selecione **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="164b7-174">In hello left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="164b7-175">![Logon Único](./media/active-directory-saas-itrp-tutorial/ic775571.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="164b7-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="164b7-176">Olá a seção de configuração de logon único, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="164b7-176">In hello Single Sign-On configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="164b7-177">![Logon Único](./media/active-directory-saas-itrp-tutorial/ic775572.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="164b7-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="164b7-178">![Logon Único](./media/active-directory-saas-itrp-tutorial/ic775573.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="164b7-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="164b7-179">a.</span><span class="sxs-lookup"><span data-stu-id="164b7-179">a.</span></span> <span data-ttu-id="164b7-180">Clique em **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="164b7-180">Click **Enable**.</span></span>

    <span data-ttu-id="164b7-181">b.</span><span class="sxs-lookup"><span data-stu-id="164b7-181">b.</span></span> <span data-ttu-id="164b7-182">Em **remoto URL de logoff** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="164b7-182">In **Remote Log Out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="164b7-183">c.</span><span class="sxs-lookup"><span data-stu-id="164b7-183">c.</span></span> <span data-ttu-id="164b7-184">Em **URL SSO SAML** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="164b7-184">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="164b7-185">d.In **impressão digital do certificado** caixa de texto, colar Olá **impressão digital** valor de certificado, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="164b7-185">d.In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="164b7-186">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="164b7-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="164b7-187">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="164b7-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="164b7-188">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="164b7-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="164b7-189">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="164b7-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="164b7-190">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="164b7-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="164b7-191">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="164b7-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="164b7-193">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="164b7-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="164b7-194">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="164b7-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="164b7-196">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="164b7-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="164b7-198">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="164b7-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="164b7-200">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="164b7-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="164b7-202">a.</span><span class="sxs-lookup"><span data-stu-id="164b7-202">a.</span></span> <span data-ttu-id="164b7-203">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="164b7-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="164b7-204">b.</span><span class="sxs-lookup"><span data-stu-id="164b7-204">b.</span></span> <span data-ttu-id="164b7-205">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="164b7-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="164b7-206">c.</span><span class="sxs-lookup"><span data-stu-id="164b7-206">c.</span></span> <span data-ttu-id="164b7-207">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="164b7-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="164b7-208">d.</span><span class="sxs-lookup"><span data-stu-id="164b7-208">d.</span></span> <span data-ttu-id="164b7-209">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="164b7-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="164b7-210">Criando um usuário de teste do ITRP</span><span class="sxs-lookup"><span data-stu-id="164b7-210">Creating an ITRP test user</span></span>

<span data-ttu-id="164b7-211">tooenable AD do Azure usuários toolog em tooITRP, eles devem ser provisionados no tooITRP.</span><span class="sxs-lookup"><span data-stu-id="164b7-211">tooenable Azure AD users toolog in tooITRP, they must be provisioned in tooITRP.</span></span>  

<span data-ttu-id="164b7-212">No caso de saudação do ITRP, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="164b7-212">In hello case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="164b7-213">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="164b7-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="164b7-214">Faça logon no tooyour **ITRP** locatário.</span><span class="sxs-lookup"><span data-stu-id="164b7-214">Log in tooyour **ITRP** tenant.</span></span>

2. <span data-ttu-id="164b7-215">Na barra de ferramentas de saudação na parte superior do hello, clique em **registros**.</span><span class="sxs-lookup"><span data-stu-id="164b7-215">In hello toolbar on hello top, click **Records**.</span></span>
   
    <span data-ttu-id="164b7-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="164b7-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="164b7-217">No menu pop-up de saudação, selecione **pessoas**.</span><span class="sxs-lookup"><span data-stu-id="164b7-217">From hello popup menu, select **People**.</span></span>
   
    <span data-ttu-id="164b7-218">![Pessoas](./media/active-directory-saas-itrp-tutorial/ic775587.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="164b7-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="164b7-219">Clique em **Adicionar Nova Pessoa** (“+”).</span><span class="sxs-lookup"><span data-stu-id="164b7-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="164b7-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="164b7-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="164b7-221">Na caixa de diálogo de adicionar nova pessoa hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="164b7-221">On hello Add New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="164b7-222">![Usuário](./media/active-directory-saas-itrp-tutorial/ic775577.png "Usuário")</span><span class="sxs-lookup"><span data-stu-id="164b7-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="164b7-223">a.</span><span class="sxs-lookup"><span data-stu-id="164b7-223">a.</span></span> <span data-ttu-id="164b7-224">Saudação de tipo **nome**, **Email** de uma conta válida do AAD você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="164b7-224">Type hello **Name**, **Email** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="164b7-225">b.</span><span class="sxs-lookup"><span data-stu-id="164b7-225">b.</span></span> <span data-ttu-id="164b7-226">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="164b7-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="164b7-227">Você pode usar qualquer ferramenta de criação outros ITRP usuário conta ou APIs fornecidas pelo ITRP tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="164b7-227">You can use any other ITRP user account creation tools or APIs provided by ITRP tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="164b7-228">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="164b7-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="164b7-229">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooITRP.</span><span class="sxs-lookup"><span data-stu-id="164b7-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooITRP.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="164b7-231">**tooassign Britta Simon tooITRP, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="164b7-231">**tooassign Britta Simon tooITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="164b7-232">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="164b7-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="164b7-234">Na lista de aplicativos hello, selecione **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="164b7-234">In hello applications list, select **ITRP**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="164b7-236">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="164b7-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="164b7-238">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="164b7-238">Click **Add** button.</span></span> <span data-ttu-id="164b7-239">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="164b7-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="164b7-241">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="164b7-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="164b7-242">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="164b7-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="164b7-243">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="164b7-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="164b7-244">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="164b7-244">Testing single sign-on</span></span>

<span data-ttu-id="164b7-245">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="164b7-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="164b7-246">Quando você clica em Olá ITRP bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de ITRP.</span><span class="sxs-lookup"><span data-stu-id="164b7-246">When you click hello ITRP tile in hello Access Panel, you should get automatically signed-on tooyour ITRP application.</span></span>
<span data-ttu-id="164b7-247">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="164b7-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="164b7-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="164b7-248">Additional resources</span></span>

* [<span data-ttu-id="164b7-249">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="164b7-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="164b7-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="164b7-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

