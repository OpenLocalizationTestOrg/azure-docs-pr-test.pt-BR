---
title: "Tutorial: integração do Azure Active Directory com o Jobscience | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 4a4c78aad6d324795a15a9569542afc23b4716d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="28553-103">Tutorial: Integração do Active Directory do Azure com o Jobscience</span><span class="sxs-lookup"><span data-stu-id="28553-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="28553-104">Neste tutorial, você aprenderá como toointegrate Jobscience com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="28553-104">In this tutorial, you learn how toointegrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="28553-105">Integrando o Jobscience com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="28553-105">Integrating Jobscience with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="28553-106">Você pode controlar no AD do Azure que tenha acesso tooJobscience</span><span class="sxs-lookup"><span data-stu-id="28553-106">You can control in Azure AD who has access tooJobscience</span></span>
- <span data-ttu-id="28553-107">Você pode habilitar seu usuários tooautomatically get conectado tooJobscience (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="28553-107">You can enable your users tooautomatically get signed-on tooJobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="28553-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="28553-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="28553-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="28553-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28553-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="28553-110">Prerequisites</span></span>

<span data-ttu-id="28553-111">tooconfigure integração do AD do Azure com o Jobscience, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="28553-111">tooconfigure Azure AD integration with Jobscience, you need hello following items:</span></span>

- <span data-ttu-id="28553-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="28553-112">An Azure AD subscription</span></span>
- <span data-ttu-id="28553-113">Uma assinatura habilitada para logon único do Jobscience</span><span class="sxs-lookup"><span data-stu-id="28553-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="28553-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="28553-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="28553-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="28553-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="28553-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="28553-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="28553-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="28553-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="28553-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="28553-118">Scenario description</span></span>
<span data-ttu-id="28553-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="28553-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="28553-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="28553-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="28553-121">Adicionando Jobscience da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="28553-121">Adding Jobscience from hello gallery</span></span>
2. <span data-ttu-id="28553-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="28553-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-hello-gallery"></a><span data-ttu-id="28553-123">Adicionando Jobscience da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="28553-123">Adding Jobscience from hello gallery</span></span>
<span data-ttu-id="28553-124">integração de saudação tooconfigure do Jobscience no AD do Azure, você precisa tooadd Jobscience da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="28553-124">tooconfigure hello integration of Jobscience into Azure AD, you need tooadd Jobscience from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="28553-125">**tooadd Jobscience da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="28553-125">**tooadd Jobscience from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="28553-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="28553-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="28553-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="28553-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="28553-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="28553-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="28553-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="28553-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="28553-133">Na caixa de pesquisa hello, digite **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="28553-133">In hello search box, type **Jobscience**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="28553-135">No painel de resultados de saudação, selecione **Jobscience**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="28553-135">In hello results panel, select **Jobscience**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="28553-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="28553-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="28553-138">Nesta seção, você configura e testa o logon único do Azure AD com o Jobscience, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="28553-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="28553-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Jobscience é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="28553-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jobscience is tooa user in Azure AD.</span></span> <span data-ttu-id="28553-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Jobscience precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="28553-140">In other words, a link relationship between an Azure AD user and hello related user in Jobscience needs toobe established.</span></span>

<span data-ttu-id="28553-141">No Jobscience, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="28553-141">In Jobscience, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="28553-142">tooconfigure e teste de logon único do AD do Azure com o Jobscience, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="28553-142">tooconfigure and test Azure AD single sign-on with Jobscience, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="28553-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="28553-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="28553-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="28553-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="28553-145">**[Criar um usuário de teste do Jobscience](#creating-a-jobscience-test-user)**  -toohave um equivalente do Britta Simon no Jobscience é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="28553-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - toohave a counterpart of Britta Simon in Jobscience that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="28553-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="28553-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="28553-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="28553-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="28553-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="28553-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="28553-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Jobscience.</span><span class="sxs-lookup"><span data-stu-id="28553-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="28553-150">**tooconfigure AD do Azure-logon único com o Jobscience, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="28553-150">**tooconfigure Azure AD single sign-on with Jobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="28553-151">Em Olá portal do Azure, Olá **Jobscience** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="28553-151">In hello Azure portal, on hello **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="28553-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="28553-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="28553-155">Em Olá **Jobscience domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="28553-155">On hello **Jobscience Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="28553-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`http://<company name>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="28553-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="28553-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="28553-158">This value is not real.</span></span> <span data-ttu-id="28553-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="28553-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="28553-160">Obter esse valor [equipe de suporte do cliente Jobscience](https://www.jobscience.com/support) ou do perfil SSO Olá criará que é explicado posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="28553-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from hello SSO profile you will create which is explained later in hello tutorial.</span></span> 
 
4. <span data-ttu-id="28553-161">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="28553-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="28553-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="28553-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="28553-165">Em Olá **Jobscience configuração** seção, clique em **configurar Jobscience** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="28553-165">On hello **Jobscience Configuration** section, click **Configure Jobscience** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="28553-166">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="28553-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="28553-168">Faça logon em tooyour site da empresa Jobscience como um administrador.</span><span class="sxs-lookup"><span data-stu-id="28553-168">Log in tooyour Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="28553-169">Vá muito**instalação**.</span><span class="sxs-lookup"><span data-stu-id="28553-169">Go too**Setup**.</span></span>
   
   <span data-ttu-id="28553-170">![Configuração](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="28553-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="28553-171">No painel de navegação à esquerda do hello, no hello **administrar** seção, clique em **gerenciamento de domínio** tooexpand Olá seção relacionada e, em seguida, clique em **meu domínio** tooopen Olá  **Meu domínio** página.</span><span class="sxs-lookup"><span data-stu-id="28553-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
   <span data-ttu-id="28553-172">![Meu Domínio](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Meu Domínio")</span><span class="sxs-lookup"><span data-stu-id="28553-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="28553-173">tooverify seu domínio foi configurado corretamente, certifique-se de que ela está em "**etapa 4 implantado tooUsers**" e examine seu "**minhas configurações de domínio**".</span><span class="sxs-lookup"><span data-stu-id="28553-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="28553-174">![Domínio implantado tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "tooUser domínio implantado")</span><span class="sxs-lookup"><span data-stu-id="28553-174">![Domain Deployed tooUser](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="28553-175">No site da empresa Olá Jobscience, clique em **controles de segurança**e, em seguida, clique em **configurações de logon único**.</span><span class="sxs-lookup"><span data-stu-id="28553-175">On hello Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="28553-176">![Controles de Segurança](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Controles de Segurança")</span><span class="sxs-lookup"><span data-stu-id="28553-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="28553-177">Em Olá **configurações de logon único** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="28553-177">In hello **Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="28553-178">![Configurações de Logon Único](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="28553-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="28553-179">a.</span><span class="sxs-lookup"><span data-stu-id="28553-179">a.</span></span> <span data-ttu-id="28553-180">Selecione **SAML Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="28553-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="28553-181">b.</span><span class="sxs-lookup"><span data-stu-id="28553-181">b.</span></span> <span data-ttu-id="28553-182">Clique em **Novo**.</span><span class="sxs-lookup"><span data-stu-id="28553-182">Click **New**.</span></span>

13. <span data-ttu-id="28553-183">Em Olá **Single Sign-On Editar configuração de SAML** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="28553-183">On hello **SAML Single Sign-On Setting Edit** dialog, perform hello following steps:</span></span>
    
    <span data-ttu-id="28553-184">![Configurações de Logon Único do SAML](./media/active-directory-saas-jobscience-tutorial/ic784365.png "Configurações de Logon Único do SAML")</span><span class="sxs-lookup"><span data-stu-id="28553-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="28553-185">a.</span><span class="sxs-lookup"><span data-stu-id="28553-185">a.</span></span> <span data-ttu-id="28553-186">Em Olá **nome** caixa de texto, digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="28553-186">In hello **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="28553-187">b.</span><span class="sxs-lookup"><span data-stu-id="28553-187">b.</span></span> <span data-ttu-id="28553-188">Em **emissor** caixa de texto valor Olá colar **ID da entidade SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="28553-188">In **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="28553-189">c.</span><span class="sxs-lookup"><span data-stu-id="28553-189">c.</span></span> <span data-ttu-id="28553-190">Em Olá **Id da entidade** caixa de texto, tipo`https://salesforce-jobscience.com`</span><span class="sxs-lookup"><span data-stu-id="28553-190">In hello **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="28553-191">d.</span><span class="sxs-lookup"><span data-stu-id="28553-191">d.</span></span> <span data-ttu-id="28553-192">Clique em **procurar** tooupload seu certificado do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="28553-192">Click **Browse** tooupload your Azure AD certificate.</span></span>

    <span data-ttu-id="28553-193">e.</span><span class="sxs-lookup"><span data-stu-id="28553-193">e.</span></span> <span data-ttu-id="28553-194">Como **tipo de identidade SAML**, selecione **asserção contém Olá ID de Federação do objeto de usuário Olá**.</span><span class="sxs-lookup"><span data-stu-id="28553-194">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>

    <span data-ttu-id="28553-195">f.</span><span class="sxs-lookup"><span data-stu-id="28553-195">f.</span></span> <span data-ttu-id="28553-196">Como **local da identidade do SAML**, selecione **identidade está no elemento Nameidentifier Olá Olá declaração assunto**.</span><span class="sxs-lookup"><span data-stu-id="28553-196">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>

    <span data-ttu-id="28553-197">g.</span><span class="sxs-lookup"><span data-stu-id="28553-197">g.</span></span> <span data-ttu-id="28553-198">Em **URL de logon do provedor de identidade** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="28553-198">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="28553-199">h.</span><span class="sxs-lookup"><span data-stu-id="28553-199">h.</span></span> <span data-ttu-id="28553-200">Em **URL de Logout do provedor de identidade** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="28553-200">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="28553-201">i.</span><span class="sxs-lookup"><span data-stu-id="28553-201">i.</span></span> <span data-ttu-id="28553-202">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="28553-202">Click **Save**.</span></span>

14. <span data-ttu-id="28553-203">No painel de navegação à esquerda do hello, no hello **administrar** seção, clique em **gerenciamento de domínio** tooexpand Olá seção relacionada e, em seguida, clique em **meu domínio** tooopen Olá  **Meu domínio** página.</span><span class="sxs-lookup"><span data-stu-id="28553-203">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="28553-204">![Meu Domínio](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Meu Domínio")</span><span class="sxs-lookup"><span data-stu-id="28553-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="28553-205">Em Olá **meu domínio** página Olá **identidade visual da página de logon** seção, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="28553-205">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="28553-206">![Identidade Visual da Página de Logon](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Identidade Visual da Página de Logon")</span><span class="sxs-lookup"><span data-stu-id="28553-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="28553-207">Em Olá **identidade visual da página de logon** página Olá **serviço de autenticação** seção, o nome de saudação do seu **configurações de SSO do SAML** é exibido.</span><span class="sxs-lookup"><span data-stu-id="28553-207">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="28553-208">Selecione-o e, em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="28553-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="28553-209">![Identidade Visual da Página de Logon](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Identidade Visual da Página de Logon")</span><span class="sxs-lookup"><span data-stu-id="28553-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="28553-210">Logon único iniciado pelo tooget Olá SP, clique em URL de logon em Olá **as configurações de logon único** em Olá **controles de segurança** seção do menu.</span><span class="sxs-lookup"><span data-stu-id="28553-210">tooget hello SP initiated Single Sign on Login URL click on hello **Single Sign On settings** in hello **Security Controls** menu section.</span></span>

    <span data-ttu-id="28553-211">![Controles de Segurança](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Controles de Segurança")</span><span class="sxs-lookup"><span data-stu-id="28553-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="28553-212">Clique em perfil Olá SSO que você criou na etapa de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="28553-212">Click hello SSO profile you have created in hello step above.</span></span> <span data-ttu-id="28553-213">Esta página mostra Olá logon único na URL para a sua empresa (por exemplo, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span><span class="sxs-lookup"><span data-stu-id="28553-213">This page shows hello Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="28553-214">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="28553-214">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="28553-215">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="28553-215">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="28553-216">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="28553-216">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="28553-217">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="28553-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="28553-218">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="28553-218">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="28553-220">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="28553-220">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="28553-221">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="28553-221">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="28553-223">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="28553-223">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="28553-225">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="28553-225">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="28553-227">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="28553-227">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="28553-229">a.</span><span class="sxs-lookup"><span data-stu-id="28553-229">a.</span></span> <span data-ttu-id="28553-230">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="28553-230">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="28553-231">b.</span><span class="sxs-lookup"><span data-stu-id="28553-231">b.</span></span> <span data-ttu-id="28553-232">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="28553-232">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="28553-233">c.</span><span class="sxs-lookup"><span data-stu-id="28553-233">c.</span></span> <span data-ttu-id="28553-234">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="28553-234">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="28553-235">d.</span><span class="sxs-lookup"><span data-stu-id="28553-235">d.</span></span> <span data-ttu-id="28553-236">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="28553-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="28553-237">Criando um usuário de teste do Jobscience</span><span class="sxs-lookup"><span data-stu-id="28553-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="28553-238">Ordem tooenable AD do Azure usuários toolog em tooJobscience, eles devem ser provisionados no Jobscience.</span><span class="sxs-lookup"><span data-stu-id="28553-238">In order tooenable Azure AD users toolog in tooJobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="28553-239">No caso de saudação do Jobscience, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="28553-239">In hello case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="28553-240">Você pode usar qualquer ferramenta de criação outros Jobscience usuário conta ou APIs fornecidas pela Jobscience tooprovision Azure Active Directory as contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="28553-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience tooprovision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="28553-241">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="28553-241">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="28553-242">Faça logon no tooyour **Jobscience** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="28553-242">Log in tooyour **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="28553-243">Vá tooSetup.</span><span class="sxs-lookup"><span data-stu-id="28553-243">Go tooSetup.</span></span>
   
   <span data-ttu-id="28553-244">![Configuração](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="28553-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="28553-245">Vá muito**gerenciar usuários \> usuários**.</span><span class="sxs-lookup"><span data-stu-id="28553-245">Go too**Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="28553-246">![Usuários](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="28553-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="28553-247">Clique em **Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="28553-247">Click **New User**.</span></span>
   
   <span data-ttu-id="28553-248">![Todos os Usuários](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Todos os Usuários")</span><span class="sxs-lookup"><span data-stu-id="28553-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="28553-249">Em Olá **Editar usuário** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="28553-249">On hello **Edit User** dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="28553-250">![Editar Usuário](./media/active-directory-saas-jobscience-tutorial/ic784371.png "Editar Usuário")</span><span class="sxs-lookup"><span data-stu-id="28553-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="28553-251">a.</span><span class="sxs-lookup"><span data-stu-id="28553-251">a.</span></span> <span data-ttu-id="28553-252">Em Olá **nome** caixa de texto, digite um nome de usuário, Olá como Britta.</span><span class="sxs-lookup"><span data-stu-id="28553-252">In hello **First Name** textbox, type a first name of hello user like Britta.</span></span>
   
   <span data-ttu-id="28553-253">b.</span><span class="sxs-lookup"><span data-stu-id="28553-253">b.</span></span> <span data-ttu-id="28553-254">Em Olá **Sobrenome** caixa de texto, digite um sobrenome do usuário hello como Simon.</span><span class="sxs-lookup"><span data-stu-id="28553-254">In hello **Last Name** textbox, type a last name of hello user like Simon.</span></span>
   
   <span data-ttu-id="28553-255">c.</span><span class="sxs-lookup"><span data-stu-id="28553-255">c.</span></span> <span data-ttu-id="28553-256">Em Olá **Alias** caixa de texto, digite um nome de alias do usuário hello como brittas.</span><span class="sxs-lookup"><span data-stu-id="28553-256">In hello **Alias** textbox, type an alias name of hello user like brittas.</span></span>

   <span data-ttu-id="28553-257">d.</span><span class="sxs-lookup"><span data-stu-id="28553-257">d.</span></span> <span data-ttu-id="28553-258">Em Olá **Email** caixa de texto, como o endereço de email do tipo saudação do usuário Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="28553-258">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="28553-259">e.</span><span class="sxs-lookup"><span data-stu-id="28553-259">e.</span></span> <span data-ttu-id="28553-260">Em Olá **nome de usuário** caixa de texto, digite um nome de usuário do usuário, como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="28553-260">In hello **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="28553-261">f.</span><span class="sxs-lookup"><span data-stu-id="28553-261">f.</span></span> <span data-ttu-id="28553-262">Em Olá **apelido** caixa de texto, digite um nome de usuário como Simon de nick.</span><span class="sxs-lookup"><span data-stu-id="28553-262">In hello **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="28553-263">g.</span><span class="sxs-lookup"><span data-stu-id="28553-263">g.</span></span> <span data-ttu-id="28553-264">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="28553-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="28553-265">proprietário de conta do Active Directory do Azure Olá recebe um email e segue um link tooconfirm sua conta antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="28553-265">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="28553-266">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="28553-266">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="28553-267">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooJobscience.</span><span class="sxs-lookup"><span data-stu-id="28553-267">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJobscience.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="28553-269">**tooassign Britta Simon tooJobscience, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="28553-269">**tooassign Britta Simon tooJobscience, perform hello following steps:**</span></span>

1. <span data-ttu-id="28553-270">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="28553-270">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="28553-272">Na lista de aplicativos hello, selecione **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="28553-272">In hello applications list, select **Jobscience**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="28553-274">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="28553-274">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="28553-276">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="28553-276">Click **Add** button.</span></span> <span data-ttu-id="28553-277">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="28553-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="28553-279">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="28553-279">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="28553-280">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="28553-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="28553-281">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="28553-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="28553-282">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="28553-282">Testing single sign-on</span></span>

<span data-ttu-id="28553-283">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="28553-283">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="28553-284">Quando você clica em bloco Jobscience Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Jobscience aplicativo.</span><span class="sxs-lookup"><span data-stu-id="28553-284">When you click hello Jobscience tile in hello Access Panel, you should get automatically signed-on tooyour Jobscience application.</span></span>
<span data-ttu-id="28553-285">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="28553-285">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="28553-286">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="28553-286">Additional resources</span></span>

* [<span data-ttu-id="28553-287">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="28553-287">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="28553-288">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="28553-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

