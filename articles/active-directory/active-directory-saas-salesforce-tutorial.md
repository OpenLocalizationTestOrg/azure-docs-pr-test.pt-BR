---
title: "Tutorial: Integração do Azure Active Directory com o Salesforce | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 1d848518ee30910e051cdc4746c599219f3b5a3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="34f0a-103">Tutorial: Integração do Azure Active Directory com o Salesforce</span><span class="sxs-lookup"><span data-stu-id="34f0a-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="34f0a-104">Neste tutorial, você aprenderá como toointegrate Salesforce com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="34f0a-104">In this tutorial, you learn how toointegrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="34f0a-105">Integrando o Salesforce com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="34f0a-105">Integrating Salesforce with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="34f0a-106">Você pode controlar no AD do Azure que tenha acesso tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="34f0a-106">You can control in Azure AD who has access tooSalesforce</span></span>
- <span data-ttu-id="34f0a-107">Você pode habilitar seu usuários tooautomatically get conectado tooSalesforce (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="34f0a-107">You can enable your users tooautomatically get signed-on tooSalesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="34f0a-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="34f0a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="34f0a-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="34f0a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34f0a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="34f0a-110">Prerequisites</span></span>

<span data-ttu-id="34f0a-111">tooconfigure integração do AD do Azure com a equipe de vendas, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="34f0a-111">tooconfigure Azure AD integration with Salesforce, you need hello following items:</span></span>

- <span data-ttu-id="34f0a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="34f0a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="34f0a-113">Uma assinatura do Salesforce com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="34f0a-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="34f0a-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="34f0a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="34f0a-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="34f0a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="34f0a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="34f0a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="34f0a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="34f0a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="34f0a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="34f0a-118">Scenario description</span></span>
<span data-ttu-id="34f0a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="34f0a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="34f0a-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="34f0a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="34f0a-121">Adicionando a equipe de vendas da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="34f0a-121">Adding Salesforce from hello gallery</span></span>
2. <span data-ttu-id="34f0a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="34f0a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-hello-gallery"></a><span data-ttu-id="34f0a-123">Adicionando a equipe de vendas da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="34f0a-123">Adding Salesforce from hello gallery</span></span>
<span data-ttu-id="34f0a-124">integração de saudação tooconfigure da equipe de vendas no AD do Azure, você precisa tooadd Salesforce da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="34f0a-124">tooconfigure hello integration of Salesforce into Azure AD, you need tooadd Salesforce from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="34f0a-125">**tooadd Salesforce da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="34f0a-125">**tooadd Salesforce from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="34f0a-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="34f0a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="34f0a-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="34f0a-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="34f0a-131">Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="34f0a-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="34f0a-133">Na caixa de pesquisa hello, digite **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-133">In hello search box, type **Salesforce**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="34f0a-135">No painel de resultados de saudação, selecione **Salesforce**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="34f0a-135">In hello results panel, select **Salesforce**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="34f0a-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="34f0a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="34f0a-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Salesforce, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="34f0a-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="34f0a-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Salesforce é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="34f0a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Salesforce is tooa user in Azure AD.</span></span> <span data-ttu-id="34f0a-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na equipe de vendas precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="34f0a-140">In other words, a link relationship between an Azure AD user and hello related user in Salesforce needs toobe established.</span></span>

<span data-ttu-id="34f0a-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="34f0a-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Salesforce.</span></span>

<span data-ttu-id="34f0a-142">tooconfigure e teste de logon único do AD do Azure com a equipe de vendas, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="34f0a-142">tooconfigure and test Azure AD single sign-on with Salesforce, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="34f0a-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="34f0a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="34f0a-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="34f0a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="34f0a-145">**[Criar um usuário de teste do Salesforce](#creating-a-salesforce-test-user)**  -toohave um equivalente do Britta Simon no Salesforce é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="34f0a-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - toohave a counterpart of Britta Simon in Salesforce that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="34f0a-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="34f0a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="34f0a-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="34f0a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="34f0a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="34f0a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="34f0a-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo com a equipe de vendas.</span><span class="sxs-lookup"><span data-stu-id="34f0a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="34f0a-150">**tooconfigure AD do Azure-logon único com o Salesforce, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="34f0a-150">**tooconfigure Azure AD single sign-on with Salesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="34f0a-151">Em Olá portal do Azure, Olá **Salesforce** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-151">In hello Azure portal, on hello **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="34f0a-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="34f0a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="34f0a-155">Em Olá **URLs e domínio do Salesforce** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="34f0a-155">On hello **Salesforce Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="34f0a-157">Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="34f0a-157">In hello **Sign-on URL** textbox, type hello value using hello following pattern:</span></span> 
   * <span data-ttu-id="34f0a-158">Conta empresarial: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="34f0a-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="34f0a-159">Conta de desenvolvedor: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="34f0a-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="34f0a-160">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="34f0a-160">These values are not hello real.</span></span> <span data-ttu-id="34f0a-161">Atualize esses valores com URL de logon real hello.</span><span class="sxs-lookup"><span data-stu-id="34f0a-161">Update these values with hello actual Sign-on URL.</span></span> <span data-ttu-id="34f0a-162">Entre em contato com [equipe de suporte da equipe de vendas de cliente](https://help.salesforce.com/support) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="34f0a-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="34f0a-163">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="34f0a-163">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="34f0a-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="34f0a-165">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="34f0a-167">Em Olá **Salesforce configuração** seção, clique em **configurar Salesforce** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="34f0a-167">On hello **Salesforce Configuration** section, click **Configure Salesforce** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="34f0a-168">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="34f0a-168">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    <span data-ttu-id="34f0a-169">![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="34f0a-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="34f0a-170">Abra uma nova guia no seu navegador e faça logon tooyour conta de administrador do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="34f0a-170">Open a new tab in your browser and log in tooyour Salesforce administrator account.</span></span>

8.  <span data-ttu-id="34f0a-171">Em Olá **administrador** painel de navegação, clique em **controles de segurança** tooexpand Olá relacionadas a seção.</span><span class="sxs-lookup"><span data-stu-id="34f0a-171">Under hello **Administrator** navigation pane, click **Security Controls** tooexpand hello related section.</span></span> <span data-ttu-id="34f0a-172">Em seguida, clique em **Configurações de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-172">Then click **Single Sign-On Settings**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="34f0a-174">Em Olá **configurações de logon único** , clique em Olá **editar** botão.</span><span class="sxs-lookup"><span data-stu-id="34f0a-174">On hello **Single Sign-On Settings** page, click hello **Edit** button.</span></span>
    <span data-ttu-id="34f0a-175">![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="34f0a-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="34f0a-176">Se você não é possível tooenable Single Sign-On configurações para sua conta do Salesforce, talvez seja necessário toocontact [equipe de suporte da equipe de vendas de cliente](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="34f0a-176">If you are unable tooenable Single Sign-On settings for your Salesforce account, you may need toocontact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="34f0a-177">Selecione **SAML Habilitado** e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="34f0a-179">tooconfigure seu SAML único logon configurações, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-179">tooconfigure your SAML single sign-on settings, click **New**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="34f0a-181">Em Olá **Single Sign-On Editar configuração de SAML** página, faça Olá configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="34f0a-181">On hello **SAML Single Sign-On Setting Edit** page, make hello following configurations:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="34f0a-183">a.</span><span class="sxs-lookup"><span data-stu-id="34f0a-183">a.</span></span> <span data-ttu-id="34f0a-184">Para Olá **nome** , digite um nome amigável para essa configuração.</span><span class="sxs-lookup"><span data-stu-id="34f0a-184">For hello **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="34f0a-185">Fornecer um valor para **nome** preencher automaticamente Olá **nome da API** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="34f0a-185">Providing a value for **Name** automatically populate hello **API Name** textbox.</span></span>

    <span data-ttu-id="34f0a-186">b.</span><span class="sxs-lookup"><span data-stu-id="34f0a-186">b.</span></span> <span data-ttu-id="34f0a-187">Colar **ID da entidade Small** valor em Olá **emissor** campo na equipe de vendas.</span><span class="sxs-lookup"><span data-stu-id="34f0a-187">Paste **SMAL Entity ID** value into hello **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="34f0a-188">c.</span><span class="sxs-lookup"><span data-stu-id="34f0a-188">c.</span></span> <span data-ttu-id="34f0a-189">Em Olá **caixa de texto de Id de entidade**, digite seu nome de domínio do Salesforce usando saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="34f0a-189">In hello **Entity Id textbox**, type your Salesforce domain name using hello following pattern:</span></span>
      
      * <span data-ttu-id="34f0a-190">Conta empresarial: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="34f0a-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="34f0a-191">Conta de desenvolvedor: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="34f0a-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="34f0a-192">d.</span><span class="sxs-lookup"><span data-stu-id="34f0a-192">d.</span></span> <span data-ttu-id="34f0a-193">Clique em **procurar** ou **Escolher arquivo** tooopen Olá **tooUpload Escolher arquivo** caixa de diálogo, selecione seu certificado Salesforce e, em seguida, clique em **abrir**certificado de saudação tooupload.</span><span class="sxs-lookup"><span data-stu-id="34f0a-193">Click **Browse** or **Choose File** tooopen hello **Choose File tooUpload** dialog, select your Salesforce certificate, and then click **Open** tooupload hello certificate.</span></span>

    <span data-ttu-id="34f0a-194">e.</span><span class="sxs-lookup"><span data-stu-id="34f0a-194">e.</span></span> <span data-ttu-id="34f0a-195">Para **Tipo de Identidade do SAML**, selecione **A declaração contém o nome de usuário salesforce.com do Usuário**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="34f0a-196">f.</span><span class="sxs-lookup"><span data-stu-id="34f0a-196">f.</span></span> <span data-ttu-id="34f0a-197">Para **local da identidade do SAML**, selecione **identidade está no elemento NameIdentifier Olá Olá declaração do assunto**</span><span class="sxs-lookup"><span data-stu-id="34f0a-197">For **SAML Identity Location**, select **Identity is in hello NameIdentifier element of hello Subject statement**</span></span>

    <span data-ttu-id="34f0a-198">g.</span><span class="sxs-lookup"><span data-stu-id="34f0a-198">g.</span></span> <span data-ttu-id="34f0a-199">Colar **o URL de serviço de logon único** em Olá **URL de logon do provedor de identidade** campo na equipe de vendas.</span><span class="sxs-lookup"><span data-stu-id="34f0a-199">Paste **Single Sign-On Service URL** into hello **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="34f0a-200">h.</span><span class="sxs-lookup"><span data-stu-id="34f0a-200">h.</span></span> <span data-ttu-id="34f0a-201">Para **Associação de Solicitação Iniciada do Provedor de Serviço**, selecione **Redirecionamento HTTP**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="34f0a-202">i.</span><span class="sxs-lookup"><span data-stu-id="34f0a-202">i.</span></span> <span data-ttu-id="34f0a-203">Por fim, clique em **salvar** tooapply seu SAML único-configurações de logon.</span><span class="sxs-lookup"><span data-stu-id="34f0a-203">Finally, click **Save** tooapply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="34f0a-204">No painel de navegação esquerdo Olá no Salesforce, clique em **gerenciamento de domínio** tooexpand Olá seção relacionada e, em seguida, clique em **meu domínio**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-204">On hello left navigation pane in Salesforce, click **Domain Management** tooexpand hello related section, and then click **My Domain**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="34f0a-206">Role para baixo toohello **configuração de autenticação** seção e, em seguida, clique em Olá **editar** botão.</span><span class="sxs-lookup"><span data-stu-id="34f0a-206">Scroll down toohello **Authentication Configuration** section, and click hello **Edit** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="34f0a-208">Em Olá **serviço de autenticação** seção, selecione o nome amigável de saudação da sua configuração de SSO do SAML e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-208">In hello **Authentication Service** section, select hello friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="34f0a-210">Se mais de um serviço de autenticação for selecionado, os usuários são solicitado tooselect qual serviço de autenticação como toosign ao iniciar o ambiente de equipe de vendas tooyour de logon único.</span><span class="sxs-lookup"><span data-stu-id="34f0a-210">If more than one authentication service is selected, users are prompted tooselect which authentication service they like toosign in with while initiating single sign-on tooyour Salesforce environment.</span></span> <span data-ttu-id="34f0a-211">Se você não quiser toohappen, você deve **Deixe todos os outros serviços de autenticação desmarcada**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-211">If you don’t want it toohappen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="34f0a-212">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="34f0a-212">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="34f0a-213">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="34f0a-213">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="34f0a-214">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="34f0a-214">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="34f0a-215">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="34f0a-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="34f0a-216">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="34f0a-216">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="34f0a-218">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="34f0a-218">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="34f0a-219">No painel de navegação esquerdo Olá Olá **portal do Azure**, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="34f0a-219">On hello left navigation pane in hello **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="34f0a-221">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-221">toodisplay hello list of users, Go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="34f0a-223">Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="34f0a-223">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="34f0a-225">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="34f0a-225">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="34f0a-227">a.</span><span class="sxs-lookup"><span data-stu-id="34f0a-227">a.</span></span> <span data-ttu-id="34f0a-228">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-228">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="34f0a-229">b.</span><span class="sxs-lookup"><span data-stu-id="34f0a-229">b.</span></span> <span data-ttu-id="34f0a-230">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="34f0a-230">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="34f0a-231">c.</span><span class="sxs-lookup"><span data-stu-id="34f0a-231">c.</span></span> <span data-ttu-id="34f0a-232">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-232">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="34f0a-233">d.</span><span class="sxs-lookup"><span data-stu-id="34f0a-233">d.</span></span> <span data-ttu-id="34f0a-234">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="34f0a-235">Criar um usuário de teste do Salesforce</span><span class="sxs-lookup"><span data-stu-id="34f0a-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="34f0a-236">Nesta seção, é criado um usuário denominado Brenda Fernandes no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="34f0a-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="34f0a-237">O Salesforce dá suporte ao provisionamento Just-In-Time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="34f0a-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="34f0a-238">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="34f0a-238">There is no action item for you in this section.</span></span> <span data-ttu-id="34f0a-239">Se um usuário ainda não existir na equipe de vendas, um novo será criado quando você tenta tooaccess Salesforce.</span><span class="sxs-lookup"><span data-stu-id="34f0a-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt tooaccess Salesforce.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="34f0a-240">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="34f0a-240">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="34f0a-241">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="34f0a-241">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSalesforce.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="34f0a-243">**tooassign Britta Simon tooSalesforce, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="34f0a-243">**tooassign Britta Simon tooSalesforce, perform hello following steps:**</span></span>

1. <span data-ttu-id="34f0a-244">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-244">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="34f0a-246">Na lista de aplicativos hello, selecione **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-246">In hello applications list, select **Salesforce**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="34f0a-248">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-248">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="34f0a-250">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-250">Click **Add** button.</span></span> <span data-ttu-id="34f0a-251">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="34f0a-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="34f0a-253">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="34f0a-253">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="34f0a-254">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="34f0a-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="34f0a-255">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="34f0a-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="34f0a-256">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="34f0a-256">Testing single sign-on</span></span>

<span data-ttu-id="34f0a-257">tootest seu único-configurações de logon, abra Olá painel de acesso em [https://myapps.microsoft.com](https://myapps.microsoft.com/), faça logon na conta de teste hello e clique em **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="34f0a-257">tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into hello test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="34f0a-258">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="34f0a-258">Additional resources</span></span>

* [<span data-ttu-id="34f0a-259">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="34f0a-259">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="34f0a-260">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="34f0a-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="34f0a-261">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="34f0a-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

