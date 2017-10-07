---
title: "Tutorial: integração do Azure Active Directory com o xMatters OnDemand | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e xMatters OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ca0633db-4f95-432e-b3db-0168193b5ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 7cc8f9f0d8cefc8a60b9514027437ced50c66242
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-xmatters-ondemand"></a><span data-ttu-id="b7913-103">Tutorial: integração do Azure Active Directory com o xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="b7913-103">Tutorial: Azure Active Directory integration with xMatters OnDemand</span></span>

<span data-ttu-id="b7913-104">Neste tutorial, você aprenderá como toointegrate xMatters OnDemand com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="b7913-104">In this tutorial, you learn how toointegrate xMatters OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b7913-105">Integrando xMatters OnDemand com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7913-105">Integrating xMatters OnDemand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b7913-106">Você pode controlar no AD do Azure que tenha acesso tooxMatters sob demanda</span><span class="sxs-lookup"><span data-stu-id="b7913-106">You can control in Azure AD who has access tooxMatters OnDemand</span></span>
- <span data-ttu-id="b7913-107">Você pode habilitar seus usuários tooautomatically get conectado tooxMatters OnDemand (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b7913-107">You can enable your users tooautomatically get signed-on tooxMatters OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b7913-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b7913-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b7913-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b7913-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7913-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b7913-110">Prerequisites</span></span>

<span data-ttu-id="b7913-111">tooconfigure integração do AD do Azure com o xMatters OnDemand, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7913-111">tooconfigure Azure AD integration with xMatters OnDemand, you need hello following items:</span></span>

- <span data-ttu-id="b7913-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b7913-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b7913-113">Uma assinatura do xMatters OnDemand habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="b7913-113">A xMatters OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b7913-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b7913-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b7913-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b7913-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b7913-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b7913-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b7913-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b7913-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b7913-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b7913-118">Scenario description</span></span>
<span data-ttu-id="b7913-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b7913-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b7913-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="b7913-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b7913-121">Adicionando xMatters OnDemand da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b7913-121">Adding xMatters OnDemand from hello gallery</span></span>
2. <span data-ttu-id="b7913-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b7913-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-xmatters-ondemand-from-hello-gallery"></a><span data-ttu-id="b7913-123">Adicionando xMatters OnDemand da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b7913-123">Adding xMatters OnDemand from hello gallery</span></span>
<span data-ttu-id="b7913-124">integração de saudação tooconfigure do xMatters OnDemand no AD do Azure, você precisa tooadd xMatters OnDemand na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="b7913-124">tooconfigure hello integration of xMatters OnDemand into Azure AD, you need tooadd xMatters OnDemand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b7913-125">**tooadd xMatters OnDemand da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b7913-125">**tooadd xMatters OnDemand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7913-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b7913-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b7913-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b7913-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b7913-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b7913-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="b7913-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b7913-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="b7913-133">Na caixa de pesquisa hello, digite **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="b7913-133">In hello search box, type **xMatters OnDemand**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_search.png)

5. <span data-ttu-id="b7913-135">No painel de resultados de saudação, selecione **xMatters OnDemand**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b7913-135">In hello results panel, select **xMatters OnDemand**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b7913-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b7913-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b7913-138">Nesta seção, você configurará e testará o logon único do Azure AD com o xMatters OnDemand com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="b7913-138">In this section, you configure and test Azure AD single sign-on with xMatters OnDemand based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b7913-139">Para toowork de logon único, AD do Azure precisa tooknow quais Olá usuário correspondente no xMatters OnDemand é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b7913-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in xMatters OnDemand is tooa user in Azure AD.</span></span> <span data-ttu-id="b7913-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no xMatters OnDemand precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="b7913-140">In other words, a link relationship between an Azure AD user and hello related user in xMatters OnDemand needs toobe established.</span></span>

<span data-ttu-id="b7913-141">No xMatters OnDemand, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7913-141">In xMatters OnDemand, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b7913-142">tooconfigure e teste de logon único do AD do Azure com o xMatters OnDemand, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7913-142">tooconfigure and test Azure AD single sign-on with xMatters OnDemand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b7913-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b7913-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b7913-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b7913-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b7913-145">**[Criar um usuário de teste do xMatters OnDemand](#creating-a-xmatters-ondemand-test-user)**  -toohave um equivalente do Britta Simon no xMatters OnDemand é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="b7913-145">**[Creating a xMatters OnDemand test user](#creating-a-xmatters-ondemand-test-user)** - toohave a counterpart of Britta Simon in xMatters OnDemand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b7913-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="b7913-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b7913-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="b7913-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b7913-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b7913-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b7913-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no seu xMatters OnDemand aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b7913-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your xMatters OnDemand application.</span></span>

<span data-ttu-id="b7913-150">**tooconfigure AD do Azure-logon único com o xMatters OnDemand, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b7913-150">**tooconfigure Azure AD single sign-on with xMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7913-151">Em Olá portal do Azure, Olá **xMatters OnDemand** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="b7913-151">In hello Azure portal, on hello **xMatters OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="b7913-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="b7913-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_samlbase.png)

3. <span data-ttu-id="b7913-155">Em Olá **xMatters OnDemand domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7913-155">On hello **xMatters OnDemand Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_url.png)
    
    <span data-ttu-id="b7913-157">a.</span><span class="sxs-lookup"><span data-stu-id="b7913-157">a.</span></span> <span data-ttu-id="b7913-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7913-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>   
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au/`|
    | `https://<companyname>.cs1.xmatters.com/`|
    | `https://<companyname>.xmatters.com/`|
    | `https://www.xmatters.com`|
    | `https://<companyname>.xmatters.com.au/`|

    <span data-ttu-id="b7913-159">b.</span><span class="sxs-lookup"><span data-stu-id="b7913-159">b.</span></span> <span data-ttu-id="b7913-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7913-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.au1.xmatters.com.au`|
    | `https://<companyname>.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.cs1.xmatters.com/sp/<instancename>`|
    | `https://<companyname>.au1.xmatters.com.au/<instancename>`|

    > [!NOTE] 
    > <span data-ttu-id="b7913-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="b7913-161">These values are not real.</span></span> <span data-ttu-id="b7913-162">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7913-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="b7913-163">Entre em contato com [equipe de suporte do xMatters OnDemand](https://www.xmatters.com/company/contact-us/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="b7913-163">Contact [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="b7913-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado do hello localmente como **c:\\XMatters OnDemand.cer**.</span><span class="sxs-lookup"><span data-stu-id="b7913-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file locally as **c:\\XMatters OnDemand.cer**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_certificate.png)
    
    > [!IMPORTANT]
    > <span data-ttu-id="b7913-166">Você precisa tooforward Olá certificado toohello [equipe de suporte do xMatters OnDemand](https://www.xmatters.com/company/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="b7913-166">You need tooforward hello certificate toohello [xMatters OnDemand support team](https://www.xmatters.com/company/contact-us/).</span></span> <span data-ttu-id="b7913-167">certificado Olá precisa toobe carregado pela equipe de suporte de xMatters Olá antes de finalizar a configuração de logon único hello.</span><span class="sxs-lookup"><span data-stu-id="b7913-167">hello certificate needs toobe uploaded by hello xMatters support team before you can finalize hello single sign-on configuration.</span></span> 

5. <span data-ttu-id="b7913-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="b7913-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b7913-170">Em Olá **xMatters OnDemand configuração** seção, clique em **configurar xMatters OnDemand** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="b7913-170">On hello **xMatters OnDemand Configuration** section, click **Configure xMatters OnDemand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b7913-171">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="b7913-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_configure.png) 

7. <span data-ttu-id="b7913-173">Em uma janela do navegador web diferente, faça logon no tooyour site da empresa XMatters OnDemand como um administrador.</span><span class="sxs-lookup"><span data-stu-id="b7913-173">In a different web browser window, log in tooyour XMatters OnDemand company site as an administrator.</span></span>

8. <span data-ttu-id="b7913-174">Na barra de ferramentas de saudação na parte superior do hello, clique em **Admin**e, em seguida, clique em **detalhes da empresa** na barra de navegação Olá Olá lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="b7913-174">In hello toolbar on hello top, click **Admin**, and then click **Company Details** in hello navigation bar on hello left side.</span></span>
   
    <span data-ttu-id="b7913-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="b7913-175">![Admin](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776795.png "Admin")</span></span>

9. <span data-ttu-id="b7913-176">Em Olá **configuração SAML** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7913-176">On hello **SAML Configuration** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="b7913-177">![Configuração SAML](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "Configuração SAML")</span><span class="sxs-lookup"><span data-stu-id="b7913-177">![SAML configuration](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776796.png "SAML configuration")</span></span>
   
    <span data-ttu-id="b7913-178">a.</span><span class="sxs-lookup"><span data-stu-id="b7913-178">a.</span></span> <span data-ttu-id="b7913-179">Selecione **Habilitar SAML**.</span><span class="sxs-lookup"><span data-stu-id="b7913-179">Select **Enable SAML**.</span></span>
   
    <span data-ttu-id="b7913-180">b.</span><span class="sxs-lookup"><span data-stu-id="b7913-180">b.</span></span> <span data-ttu-id="b7913-181">Colar **ID da entidade SAML**, que você copiou de saudação portal do Azure em hello **ID do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="b7913-181">Paste **SAML Entity ID**, which you have copied from hello Azure portal into hello **Identity Provider ID** textbox.</span></span>
   
    <span data-ttu-id="b7913-182">c.</span><span class="sxs-lookup"><span data-stu-id="b7913-182">c.</span></span> <span data-ttu-id="b7913-183">Colar **Single Sign-On URL do serviço SAML**, que você copiou de saudação portal do Azure em hello **URL de logon único** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="b7913-183">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **Single Sign On URL** textbox.</span></span>
   
    <span data-ttu-id="b7913-184">d.</span><span class="sxs-lookup"><span data-stu-id="b7913-184">d.</span></span> <span data-ttu-id="b7913-185">Colar **URL de logout**, que você copiou de saudação portal do Azure em hello **URL de Logout único** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="b7913-185">Paste **Sign-Out URL**, which you have copied from hello Azure portal into hello **Single Logout URL** textbox.</span></span>
   
    <span data-ttu-id="b7913-186">e.</span><span class="sxs-lookup"><span data-stu-id="b7913-186">e.</span></span> <span data-ttu-id="b7913-187">Na página de detalhes da empresa hello, na parte superior da saudação, clique em **salvar alterações**.</span><span class="sxs-lookup"><span data-stu-id="b7913-187">On hello Company Details page, at hello top, click **Save Changes**.</span></span>
    
    <span data-ttu-id="b7913-188">![Detalhes da empresa](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Detalhes da empresa")</span><span class="sxs-lookup"><span data-stu-id="b7913-188">![Company details](./media/active-directory-saas-xmatters-ondemand-tutorial/IC776797.png "Company details")</span></span>

> [!TIP]
> <span data-ttu-id="b7913-189">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="b7913-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b7913-190">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="b7913-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b7913-191">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b7913-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b7913-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b7913-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="b7913-193">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b7913-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="b7913-195">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b7913-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7913-196">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b7913-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b7913-198">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="b7913-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b7913-200">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7913-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b7913-202">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7913-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-xmatters-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b7913-204">a.</span><span class="sxs-lookup"><span data-stu-id="b7913-204">a.</span></span> <span data-ttu-id="b7913-205">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b7913-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b7913-206">b.</span><span class="sxs-lookup"><span data-stu-id="b7913-206">b.</span></span> <span data-ttu-id="b7913-207">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b7913-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b7913-208">c.</span><span class="sxs-lookup"><span data-stu-id="b7913-208">c.</span></span> <span data-ttu-id="b7913-209">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="b7913-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b7913-210">d.</span><span class="sxs-lookup"><span data-stu-id="b7913-210">d.</span></span> <span data-ttu-id="b7913-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b7913-211">Click **Create**.</span></span>
 
### <a name="creating-a-xmatters-ondemand-test-user"></a><span data-ttu-id="b7913-212">Criação de um usuário de teste do xMatters OnDemand</span><span class="sxs-lookup"><span data-stu-id="b7913-212">Creating a xMatters OnDemand test user</span></span>

<span data-ttu-id="b7913-213">Em ordem tooenable AD do Azure usuários toolog em tooXMatters OnDemand, eles devem ser provisionados no XMatters OnDemand.</span><span class="sxs-lookup"><span data-stu-id="b7913-213">In order tooenable Azure AD users toolog in tooXMatters OnDemand, they must be provisioned into XMatters OnDemand.</span></span> <span data-ttu-id="b7913-214">No caso de saudação do XMatters OnDemand, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="b7913-214">In hello case of XMatters OnDemand, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-accounts-perform-hello-following-steps"></a><span data-ttu-id="b7913-215">tooprovision contas de usuário, executar Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b7913-215">tooprovision a user accounts, perform hello following steps:</span></span>
1. <span data-ttu-id="b7913-216">Faça logon no tooyour **XMatters OnDemand** locatário.</span><span class="sxs-lookup"><span data-stu-id="b7913-216">Log in tooyour **XMatters OnDemand** tenant.</span></span>

2.  <span data-ttu-id="b7913-217">Clique em **usuários** na guia e clique **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="b7913-217">Click **Users** tab. and then click **Add User**.</span></span>
  
    <span data-ttu-id="b7913-218">![Usuários](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="b7913-218">![Users](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781048.png "Users")</span></span>

3. <span data-ttu-id="b7913-219">Em Olá **adicionar um usuário** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7913-219">In hello **Add a User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="b7913-220">![Adicionar um Usuário](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Adicionar um Usuário")</span><span class="sxs-lookup"><span data-stu-id="b7913-220">![Add a User](./media/active-directory-saas-xmatters-ondemand-tutorial/IC781049.png "Add a User")</span></span>

    <span data-ttu-id="b7913-221">a.</span><span class="sxs-lookup"><span data-stu-id="b7913-221">a.</span></span> <span data-ttu-id="b7913-222">Selecione **Ativo**.</span><span class="sxs-lookup"><span data-stu-id="b7913-222">Select **Active**.</span></span>

    <span data-ttu-id="b7913-223">b.</span><span class="sxs-lookup"><span data-stu-id="b7913-223">b.</span></span> <span data-ttu-id="b7913-224">Em Olá **ID de usuário** caixa de texto, id de usuário do tipo saudação do usuário como Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="b7913-224">In hello **User ID** textbox, type hello user id of user like Brittasimon@contoso.com.</span></span>
   
    <span data-ttu-id="b7913-225">c.</span><span class="sxs-lookup"><span data-stu-id="b7913-225">c.</span></span> <span data-ttu-id="b7913-226">Em Olá **nome** caixa de texto Nome do primeiro tipo de usuário hello como Britta.</span><span class="sxs-lookup"><span data-stu-id="b7913-226">In hello **First Name** textbox, type first name of hello user like Britta.</span></span>

    <span data-ttu-id="b7913-227">d.</span><span class="sxs-lookup"><span data-stu-id="b7913-227">d.</span></span> <span data-ttu-id="b7913-228">Em Olá **Sobrenome** caixa de texto, digite sobrenome do usuário hello como Simon.</span><span class="sxs-lookup"><span data-stu-id="b7913-228">In hello **Last Name** textbox, type last name of hello user like Simon.</span></span>
    
    <span data-ttu-id="b7913-229">e.</span><span class="sxs-lookup"><span data-stu-id="b7913-229">e.</span></span> <span data-ttu-id="b7913-230">Em Olá **Site** caixa de texto, digite site válido do hello de um válida do Azure você deseja tooprovision de conta do AD.</span><span class="sxs-lookup"><span data-stu-id="b7913-230">In hello **Site** textbox, Enter hello valid site of a valid Azure AD account you want tooprovision.</span></span>
    
    <span data-ttu-id="b7913-231">f.</span><span class="sxs-lookup"><span data-stu-id="b7913-231">f.</span></span> <span data-ttu-id="b7913-232">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="b7913-232">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b7913-233">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b7913-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b7913-234">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooxMatters sob demanda.</span><span class="sxs-lookup"><span data-stu-id="b7913-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooxMatters OnDemand.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="b7913-236">**tooassign Britta Simon tooxMatters OnDemand, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b7913-236">**tooassign Britta Simon tooxMatters OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="b7913-237">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b7913-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="b7913-239">Na lista de aplicativos hello, selecione **xMatters OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="b7913-239">In hello applications list, select **xMatters OnDemand**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_xmattersondemand_app.png) 

3. <span data-ttu-id="b7913-241">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b7913-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="b7913-243">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b7913-243">Click **Add** button.</span></span> <span data-ttu-id="b7913-244">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b7913-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="b7913-246">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7913-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b7913-247">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b7913-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b7913-248">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b7913-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b7913-249">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="b7913-249">Testing single sign-on</span></span>

<span data-ttu-id="b7913-250">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7913-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b7913-251">Quando você clica em Olá xMatters OnDemand lado a lado no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour xMatters OnDemand aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b7913-251">When you click hello xMatters OnDemand tile in hello Access Panel, you should get automatically signed-on tooyour xMatters OnDemand application.</span></span>
<span data-ttu-id="b7913-252">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b7913-252">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b7913-253">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b7913-253">Additional resources</span></span>

* [<span data-ttu-id="b7913-254">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b7913-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b7913-255">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b7913-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-xmatters-ondemand-tutorial/tutorial_general_203.png

