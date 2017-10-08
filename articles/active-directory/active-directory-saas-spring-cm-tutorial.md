---
title: "Tutorial: Integração do Azure Active Directory com o SpringCM | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o SpringCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4a42f797-ac58-4aca-a8e6-53bfe5529083
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 12c8ebe765e2c6e61115256e9343d90ec132e1f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-springcm"></a><span data-ttu-id="3ff13-103">Tutorial: Integração do Azure Active Directory com o SpringCM</span><span class="sxs-lookup"><span data-stu-id="3ff13-103">Tutorial: Azure Active Directory integration with SpringCM</span></span>

<span data-ttu-id="3ff13-104">Neste tutorial, você aprenderá como toointegrate SpringCM com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="3ff13-104">In this tutorial, you learn how toointegrate SpringCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ff13-105">Integrando o SpringCM com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ff13-105">Integrating SpringCM with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3ff13-106">Você pode controlar no AD do Azure que tenha acesso tooSpringCM</span><span class="sxs-lookup"><span data-stu-id="3ff13-106">You can control in Azure AD who has access tooSpringCM</span></span>
- <span data-ttu-id="3ff13-107">Você pode habilitar seu usuários tooautomatically get conectado tooSpringCM (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ff13-107">You can enable your users tooautomatically get signed-on tooSpringCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ff13-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3ff13-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3ff13-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3ff13-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ff13-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3ff13-110">Prerequisites</span></span>

<span data-ttu-id="3ff13-111">tooconfigure integração do AD do Azure com SpringCM, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ff13-111">tooconfigure Azure AD integration with SpringCM, you need hello following items:</span></span>

- <span data-ttu-id="3ff13-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ff13-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3ff13-113">Uma assinatura habilitada para logon único do SpringCM</span><span class="sxs-lookup"><span data-stu-id="3ff13-113">A SpringCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ff13-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3ff13-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ff13-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3ff13-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ff13-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3ff13-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ff13-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ff13-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ff13-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3ff13-118">Scenario description</span></span>
<span data-ttu-id="3ff13-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3ff13-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ff13-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="3ff13-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ff13-121">Adicionando SpringCM da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3ff13-121">Adding SpringCM from hello gallery</span></span>
2. <span data-ttu-id="3ff13-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ff13-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-springcm-from-hello-gallery"></a><span data-ttu-id="3ff13-123">Adicionando SpringCM da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3ff13-123">Adding SpringCM from hello gallery</span></span>
<span data-ttu-id="3ff13-124">integração de saudação tooconfigure do SpringCM no AD do Azure, você precisa tooadd SpringCM da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3ff13-124">tooconfigure hello integration of SpringCM into Azure AD, you need tooadd SpringCM from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3ff13-125">**tooadd SpringCM da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3ff13-125">**tooadd SpringCM from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ff13-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3ff13-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ff13-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3ff13-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3ff13-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3ff13-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3ff13-133">Na caixa de pesquisa hello, digite **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-133">In hello search box, type **SpringCM**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_search.png)

5. <span data-ttu-id="3ff13-135">No painel de resultados de saudação, selecione **SpringCM**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3ff13-135">In hello results panel, select **SpringCM**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3ff13-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ff13-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3ff13-138">Nesta seção, você configurará e testará o logon único do Azure AD com o SpringCM com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3ff13-138">In this section, you configure and test Azure AD single sign-on with SpringCM based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3ff13-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no SpringCM é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ff13-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SpringCM is tooa user in Azure AD.</span></span> <span data-ttu-id="3ff13-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no SpringCM precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="3ff13-140">In other words, a link relationship between an Azure AD user and hello related user in SpringCM needs toobe established.</span></span>

<span data-ttu-id="3ff13-141">No SpringCM, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="3ff13-141">In SpringCM, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3ff13-142">tooconfigure e teste de logon único do AD do Azure com SpringCM, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ff13-142">tooconfigure and test Azure AD single sign-on with SpringCM, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3ff13-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3ff13-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3ff13-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ff13-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ff13-145">**[Criar um usuário de teste do SpringCM](#creating-a-springcm-test-user)**  -toohave um equivalente do Britta Simon no SpringCM é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="3ff13-145">**[Creating a SpringCM test user](#creating-a-springcm-test-user)** - toohave a counterpart of Britta Simon in SpringCM that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3ff13-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="3ff13-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ff13-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="3ff13-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3ff13-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ff13-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3ff13-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo SpringCM.</span><span class="sxs-lookup"><span data-stu-id="3ff13-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SpringCM application.</span></span>

<span data-ttu-id="3ff13-150">**tooconfigure AD do Azure-logon único com SpringCM, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3ff13-150">**tooconfigure Azure AD single sign-on with SpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ff13-151">Em Olá portal do Azure, Olá **SpringCM** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-151">In hello Azure portal, on hello **SpringCM** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3ff13-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="3ff13-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_samlbase.png)

3. <span data-ttu-id="3ff13-155">Em Olá **SpringCM domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ff13-155">On hello **SpringCM Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_url.png)

    <span data-ttu-id="3ff13-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span><span class="sxs-lookup"><span data-stu-id="3ff13-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://na11.springcm.com/atlas/SSO/SSOEndpoint.ashx?aid=<identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3ff13-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="3ff13-158">This value is not real.</span></span> <span data-ttu-id="3ff13-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="3ff13-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="3ff13-160">Entre em contato com [equipe de suporte do cliente do SpringCM](https://knowledge.springcm.com/support) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="3ff13-160">Contact [SpringCM Client support team](https://knowledge.springcm.com/support) tooget this value.</span></span> 
 
4. <span data-ttu-id="3ff13-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Raw)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3ff13-161">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_certificate.png) 

5. <span data-ttu-id="3ff13-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3ff13-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-spring-cm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3ff13-165">Em Olá **SpringCM configuração** seção, clique em **configurar SpringCM** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="3ff13-165">On hello **SpringCM Configuration** section, click **Configure SpringCM** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3ff13-166">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="3ff13-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_configure.png)   

7. <span data-ttu-id="3ff13-168">Em uma janela de navegador web diferente, logon tooyour **SpringCM** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="3ff13-168">In a different web browser window, sign on tooyour **SpringCM** company site as administrator.</span></span>

8. <span data-ttu-id="3ff13-169">No menu de saudação na parte superior de saudação, clique em **ir para**, clique em **preferências**e em seguida, no hello **preferências da conta** seção, clique em **SSO do SAML**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-169">In hello menu on hello top, click **GO TO**, click **Preferences**, and then, in hello **Account Preferences** section, click **SAML SSO**.</span></span>
   
    <span data-ttu-id="3ff13-170">![SSO do SAML](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SSO do SAML")</span><span class="sxs-lookup"><span data-stu-id="3ff13-170">![SAML SSO](./media/active-directory-saas-spring-cm-tutorial/ic797051.png "SAML SSO")</span></span>

9. <span data-ttu-id="3ff13-171">Na seção de configuração do provedor de identidade do hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ff13-171">In hello Identity Provider Configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="3ff13-172">![Configuração do Provedor de Identidade](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Configuração do Provedor de Identidade")</span><span class="sxs-lookup"><span data-stu-id="3ff13-172">![Identity Provider Configuration](./media/active-directory-saas-spring-cm-tutorial/ic797052.png "Identity Provider Configuration")</span></span>
    
    <span data-ttu-id="3ff13-173">a.</span><span class="sxs-lookup"><span data-stu-id="3ff13-173">a.</span></span> <span data-ttu-id="3ff13-174">tooupload seu certificado baixado do Active Directory do Azure, clique em **Selecionar certificado do emissor** ou **alterar certificado do emissor**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-174">tooupload your downloaded Azure Active Directory certificate, click **Select Issuer Certificate** or **Change Issuer Certificate**.</span></span>
    
    <span data-ttu-id="3ff13-175">b.</span><span class="sxs-lookup"><span data-stu-id="3ff13-175">b.</span></span> <span data-ttu-id="3ff13-176">Colar **ID da entidade SAML** valor que você copiou do portal do Azure em Olá **emissor** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3ff13-176">Paste **SAML Entity ID** value, which you have copied from Azure portal into hello **Issuer** textbox.</span></span>
    
    <span data-ttu-id="3ff13-177">c.</span><span class="sxs-lookup"><span data-stu-id="3ff13-177">c.</span></span> <span data-ttu-id="3ff13-178">Colar **Single Sign-On URL do serviço SAML** valor que você copiou de saudação portal do Azure em hello **ponto de extremidade iniciado do provedor de serviço (SP)** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3ff13-178">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Service Provider (SP) Initiated Endpoint** textbox.</span></span>
            
    <span data-ttu-id="3ff13-179">d.</span><span class="sxs-lookup"><span data-stu-id="3ff13-179">d.</span></span> <span data-ttu-id="3ff13-180">Selecione **SAML Habilitado** como **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-180">Select **SAML Enabled** as **Enable**.</span></span>

    <span data-ttu-id="3ff13-181">e.</span><span class="sxs-lookup"><span data-stu-id="3ff13-181">e.</span></span> <span data-ttu-id="3ff13-182">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-182">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="3ff13-183">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="3ff13-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3ff13-184">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="3ff13-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3ff13-185">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3ff13-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3ff13-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ff13-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="3ff13-187">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3ff13-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3ff13-189">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3ff13-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ff13-190">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3ff13-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3ff13-192">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3ff13-194">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3ff13-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ff13-196">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3ff13-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-spring-cm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3ff13-198">a.</span><span class="sxs-lookup"><span data-stu-id="3ff13-198">a.</span></span> <span data-ttu-id="3ff13-199">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ff13-200">b.</span><span class="sxs-lookup"><span data-stu-id="3ff13-200">b.</span></span> <span data-ttu-id="3ff13-201">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3ff13-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3ff13-202">c.</span><span class="sxs-lookup"><span data-stu-id="3ff13-202">c.</span></span> <span data-ttu-id="3ff13-203">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3ff13-204">d.</span><span class="sxs-lookup"><span data-stu-id="3ff13-204">d.</span></span> <span data-ttu-id="3ff13-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-205">Click **Create**.</span></span>
 
### <a name="creating-a-springcm-test-user"></a><span data-ttu-id="3ff13-206">Criar um usuário de teste do SpringCM</span><span class="sxs-lookup"><span data-stu-id="3ff13-206">Creating a SpringCM test user</span></span>

<span data-ttu-id="3ff13-207">toolog de usuários do Active Directory do Azure tooenable em tooSpringCM, eles devem ser provisionados no SpringCM.</span><span class="sxs-lookup"><span data-stu-id="3ff13-207">tooenable Azure Active Directory users toolog in tooSpringCM, they must be provisioned into SpringCM.</span></span> <span data-ttu-id="3ff13-208">No caso de saudação do SpringCM, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="3ff13-208">In hello case of SpringCM, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="3ff13-209">Para obter mais informações, veja [Criar e editar um usuário do SpringCM](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span><span class="sxs-lookup"><span data-stu-id="3ff13-209">For more information, see [Create and Edit a SpringCM User](http://knowledge.springcm.com/create-and-edit-a-springcm-user).</span></span> 

<span data-ttu-id="3ff13-210">**tooprovision um tooSpringCM de conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3ff13-210">**tooprovision a user account tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ff13-211">Faça logon no tooyour **SpringCM** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="3ff13-211">Log in tooyour **SpringCM** company site as administrator.</span></span>

2. <span data-ttu-id="3ff13-212">Clique em **IR PARA** e depois em **CATÁLOGO DE ENDEREÇOS**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-212">Click **GOTO**, and then click **ADDRESS BOOK**.</span></span>
   
    <span data-ttu-id="3ff13-213">![Criar usuário](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Criar usuário")</span><span class="sxs-lookup"><span data-stu-id="3ff13-213">![Create User](./media/active-directory-saas-spring-cm-tutorial/ic797054.png "Create User")</span></span>

3. <span data-ttu-id="3ff13-214">Clique em **Criar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-214">Click **Create User**.</span></span>

4. <span data-ttu-id="3ff13-215">Selecione uma **Função de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-215">Select a **User Role**.</span></span>

5. <span data-ttu-id="3ff13-216">Selecione **Enviar Email de Ativação**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-216">Select **Send Activation Email**.</span></span>

6. <span data-ttu-id="3ff13-217">Tipo hello nome, sobrenome e endereço de email de uma conta de usuário válida do Active Directory do Azure que você deseja tooprovision em Olá relacionam caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="3ff13-217">Type hello first name, last name, and email address of a valid Azure Active Directory user account you want tooprovision into hello related textboxes.</span></span>

7. <span data-ttu-id="3ff13-218">Adicionar Olá usuário tooa **grupo de segurança**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-218">Add hello user tooa **Security group**.</span></span>

8. <span data-ttu-id="3ff13-219">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-219">Click **Save**.</span></span>

  >[!NOTE]
  ><span data-ttu-id="3ff13-220">Você pode usar qualquer ferramenta de criação outros SpringCM usuário conta ou APIs fornecidas pelo SpringCM tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="3ff13-220">You can use any other SpringCM user account creation tools or APIs provided by SpringCM tooprovision AAD user accounts.</span></span>  
  > 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3ff13-221">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3ff13-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3ff13-222">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSpringCM.</span><span class="sxs-lookup"><span data-stu-id="3ff13-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSpringCM.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3ff13-224">**tooassign Britta Simon tooSpringCM, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3ff13-224">**tooassign Britta Simon tooSpringCM, perform hello following steps:**</span></span>

1. <span data-ttu-id="3ff13-225">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3ff13-227">Na lista de aplicativos hello, selecione **SpringCM**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-227">In hello applications list, select **SpringCM**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-spring-cm-tutorial/tutorial_springcm_app.png) 

3. <span data-ttu-id="3ff13-229">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3ff13-231">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3ff13-231">Click **Add** button.</span></span> <span data-ttu-id="3ff13-232">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3ff13-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3ff13-234">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="3ff13-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3ff13-235">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3ff13-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ff13-236">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3ff13-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3ff13-237">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3ff13-237">Testing single sign-on</span></span>

<span data-ttu-id="3ff13-238">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="3ff13-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="3ff13-239">Quando você clica em bloco SpringCM Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour SpringCM aplicativo.</span><span class="sxs-lookup"><span data-stu-id="3ff13-239">When you click hello SpringCM tile in hello Access Panel, you should get automatically signed-on tooyour SpringCM application.</span></span>

<span data-ttu-id="3ff13-240">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3ff13-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3ff13-241">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3ff13-241">Additional resources</span></span>

* [<span data-ttu-id="3ff13-242">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3ff13-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ff13-243">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3ff13-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-spring-cm-tutorial/tutorial_general_203.png

