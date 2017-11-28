---
title: "Tutorial: Integração do Azure Active Directory com o Zendesk | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="c8504-103">Tutorial: Integração do Active Directory do Azure com o Zendesk</span><span class="sxs-lookup"><span data-stu-id="c8504-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="c8504-104">Neste tutorial, você aprenderá como toointegrate Zendesk com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c8504-104">In this tutorial, you learn how toointegrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c8504-105">Integração do Zendesk com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8504-105">Integrating Zendesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c8504-106">Você pode controlar no AD do Azure que tenha acesso tooZendesk</span><span class="sxs-lookup"><span data-stu-id="c8504-106">You can control in Azure AD who has access tooZendesk</span></span>
- <span data-ttu-id="c8504-107">Você pode habilitar seu usuários tooautomatically get conectado tooZendesk (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8504-107">You can enable your users tooautomatically get signed-on tooZendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c8504-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c8504-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c8504-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c8504-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8504-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c8504-110">Prerequisites</span></span>

<span data-ttu-id="c8504-111">tooconfigure integração do AD do Azure com o Zendesk, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8504-111">tooconfigure Azure AD integration with Zendesk, you need hello following items:</span></span>

- <span data-ttu-id="c8504-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8504-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c8504-113">Uma assinatura habilitada para logon único do Zendesk</span><span class="sxs-lookup"><span data-stu-id="c8504-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="c8504-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c8504-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="c8504-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c8504-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c8504-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c8504-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c8504-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c8504-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="c8504-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c8504-118">Scenario description</span></span>
<span data-ttu-id="c8504-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c8504-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c8504-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c8504-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c8504-121">Adicionando Zendesk da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c8504-121">Adding Zendesk from hello gallery</span></span>
2. <span data-ttu-id="c8504-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8504-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-hello-gallery"></a><span data-ttu-id="c8504-123">Adicionando Zendesk da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c8504-123">Adding Zendesk from hello gallery</span></span>
<span data-ttu-id="c8504-124">integração de saudação tooconfigure do Zendesk no AD do Azure, você precisa tooadd Zendesk da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c8504-124">tooconfigure hello integration of Zendesk into Azure AD, you need tooadd Zendesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c8504-125">**tooadd Zendesk da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c8504-125">**tooadd Zendesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8504-126">Em Olá  **[Portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c8504-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c8504-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c8504-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c8504-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c8504-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c8504-131">Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8504-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c8504-133">Na caixa de pesquisa hello, digite **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="c8504-133">In hello search box, type **Zendesk**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="c8504-135">No painel de resultados de saudação, selecione **Zendesk**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c8504-135">In hello results panel, select **Zendesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c8504-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8504-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c8504-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Zendesk, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c8504-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c8504-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Zendesk é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8504-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zendesk is tooa user in Azure AD.</span></span> <span data-ttu-id="c8504-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Zendesk precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c8504-140">In other words, a link relationship between an Azure AD user and hello related user in Zendesk needs toobe established.</span></span>

<span data-ttu-id="c8504-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Zendesk.</span><span class="sxs-lookup"><span data-stu-id="c8504-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zendesk.</span></span>

<span data-ttu-id="c8504-142">tooconfigure e teste de logon único do AD do Azure com o Zendesk, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8504-142">tooconfigure and test Azure AD single sign-on with Zendesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c8504-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c8504-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c8504-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c8504-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c8504-145">**[Criar um usuário de teste do Zendesk](#creating-a-zendesk-test-user)**  -toohave um equivalente do Britta Simon no Zendesk é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c8504-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - toohave a counterpart of Britta Simon in Zendesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c8504-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c8504-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c8504-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c8504-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c8504-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8504-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c8504-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Zendesk.</span><span class="sxs-lookup"><span data-stu-id="c8504-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="c8504-150">**tooconfigure AD do Azure-logon único com o Zendesk, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c8504-150">**tooconfigure Azure AD single sign-on with Zendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8504-151">Em Olá portal do Azure, Olá **Zendesk** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c8504-151">In hello Azure portal, on hello **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c8504-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c8504-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="c8504-155">Em Olá **Zendesk domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8504-155">On hello **Zendesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="c8504-157">a.</span><span class="sxs-lookup"><span data-stu-id="c8504-157">a.</span></span> <span data-ttu-id="c8504-158">Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="c8504-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="c8504-159">b.</span><span class="sxs-lookup"><span data-stu-id="c8504-159">b.</span></span> <span data-ttu-id="c8504-160">Em Olá **identificador** texto, o valor do tipo hello usando saudação padrão a seguir:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="c8504-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c8504-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c8504-161">These values are not real.</span></span> <span data-ttu-id="c8504-162">Atualize esses valores com URL de logon real hello e a URL de identificador.</span><span class="sxs-lookup"><span data-stu-id="c8504-162">Update these values with hello actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="c8504-163">Entre em contato com [equipe de suporte do Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="c8504-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget these values.</span></span> 

4. <span data-ttu-id="c8504-164">Zendesk espera as asserções SAML de saudação em um formato específico.</span><span class="sxs-lookup"><span data-stu-id="c8504-164">Zendesk expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="c8504-165">Não há nenhum atributo SAML obrigatório, mas, opcionalmente, você pode adicionar um atributo de **atributos de usuário** seção Olá seguir etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8504-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following hello below steps:</span></span> 

     ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="c8504-167">a.</span><span class="sxs-lookup"><span data-stu-id="c8504-167">a.</span></span> <span data-ttu-id="c8504-168">Clique em Olá **exibir e editar Olá outros atributos** caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="c8504-168">Click hello **View and edit all hello other attributes** check box.</span></span>
     
    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="c8504-170">b.</span><span class="sxs-lookup"><span data-stu-id="c8504-170">b.</span></span> <span data-ttu-id="c8504-171">Clique em Olá **Adicionar atributo** tooopen **Adicionar atributo** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8504-171">Click hello **Add Attribute** tooopen **Add attribute** dialog.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="c8504-173">c.</span><span class="sxs-lookup"><span data-stu-id="c8504-173">c.</span></span> <span data-ttu-id="c8504-174">Em Olá **nome** caixa de texto Nome do atributo do tipo hello (por exemplo **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="c8504-174">In hello **Name** textbox, type hello attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="c8504-175">d.</span><span class="sxs-lookup"><span data-stu-id="c8504-175">d.</span></span> <span data-ttu-id="c8504-176">De saudação **valor** lista, o valor do atributo select hello (como **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="c8504-176">From hello **Value** list, select hello attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="c8504-177">e.</span><span class="sxs-lookup"><span data-stu-id="c8504-177">e.</span></span> <span data-ttu-id="c8504-178">Clique em **Ok**</span><span class="sxs-lookup"><span data-stu-id="c8504-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="c8504-179">Você usar atributos de tooadd de atributos de extensão que não estão no AD do Azure por padrão.</span><span class="sxs-lookup"><span data-stu-id="c8504-179">You use extension attributes tooadd attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="c8504-180">Clique em [atributos de usuário que podem ser definidos em SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) lista completa de saudação de tooget de SAML atributos que **Zendesk** aceita.</span><span class="sxs-lookup"><span data-stu-id="c8504-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="c8504-181">Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** o valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="c8504-181">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="c8504-183">Em Olá **Zendesk configuração** seção, clique em **configurar Zendesk** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="c8504-183">On hello **Zendesk Configuration** section, click **Configure Zendesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c8504-184">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="c8504-184">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="c8504-186">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa Zendesk como administrador.</span><span class="sxs-lookup"><span data-stu-id="c8504-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="c8504-187">Clique em **Administrador**.</span><span class="sxs-lookup"><span data-stu-id="c8504-187">Click **Admin**.</span></span>

9. <span data-ttu-id="c8504-188">No painel de navegação esquerdo hello, clique em **configurações**e, em seguida, clique em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="c8504-188">In hello left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="c8504-189">Em Olá **segurança** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8504-189">On hello **Security** page, perform hello following steps:</span></span> 
   
     <span data-ttu-id="c8504-190">![Segurança](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Segurança")</span><span class="sxs-lookup"><span data-stu-id="c8504-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="c8504-191">![Logon Único](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="c8504-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="c8504-192">a.</span><span class="sxs-lookup"><span data-stu-id="c8504-192">a.</span></span> <span data-ttu-id="c8504-193">Clique em Olá **agentes & Admin** guia.</span><span class="sxs-lookup"><span data-stu-id="c8504-193">Click hello **Admin & Agents** tab.</span></span>

     <span data-ttu-id="c8504-194">b.</span><span class="sxs-lookup"><span data-stu-id="c8504-194">b.</span></span> <span data-ttu-id="c8504-195">Selecione **SSO (logon único) e SAML** e, em seguida, selecione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="c8504-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="c8504-196">c.</span><span class="sxs-lookup"><span data-stu-id="c8504-196">c.</span></span> <span data-ttu-id="c8504-197">Em **URL SSO SAML** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8504-197">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="c8504-198">d.</span><span class="sxs-lookup"><span data-stu-id="c8504-198">d.</span></span> <span data-ttu-id="c8504-199">Em **URL de Logout remoto** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8504-199">In **Remote Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="c8504-200">e.</span><span class="sxs-lookup"><span data-stu-id="c8504-200">e.</span></span> <span data-ttu-id="c8504-201">Em **impressão digital do certificado** caixa de texto, colar Olá **impressão digital** o valor de certificado que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8504-201">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="c8504-202">f.</span><span class="sxs-lookup"><span data-stu-id="c8504-202">f.</span></span> <span data-ttu-id="c8504-203">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c8504-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c8504-204">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8504-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="c8504-205">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8504-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c8504-207">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c8504-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8504-208">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c8504-208">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c8504-210">lista de saudação toodisplay de usuários ir muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c8504-210">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c8504-212">Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8504-212">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c8504-214">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8504-214">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c8504-216">a.</span><span class="sxs-lookup"><span data-stu-id="c8504-216">a.</span></span> <span data-ttu-id="c8504-217">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c8504-217">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c8504-218">b.</span><span class="sxs-lookup"><span data-stu-id="c8504-218">b.</span></span> <span data-ttu-id="c8504-219">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c8504-219">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c8504-220">c.</span><span class="sxs-lookup"><span data-stu-id="c8504-220">c.</span></span> <span data-ttu-id="c8504-221">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c8504-221">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c8504-222">d.</span><span class="sxs-lookup"><span data-stu-id="c8504-222">d.</span></span> <span data-ttu-id="c8504-223">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c8504-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="c8504-224">Criação de um usuário de teste do Zendesk</span><span class="sxs-lookup"><span data-stu-id="c8504-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="c8504-225">toolog de usuários tooenable AD do Azure em **Zendesk**, eles devem ser provisionados no **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="c8504-225">tooenable Azure AD users toolog into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="c8504-226">Dependendo da função hello atribuída em aplicativos hello, Olá seu comportamento esperado:</span><span class="sxs-lookup"><span data-stu-id="c8504-226">Depending on hello role assigned in hello apps, it's hello expected behavior:</span></span>

 1. <span data-ttu-id="c8504-227">As contas de **Usuário final** são provisionadas automaticamente ao entrar.</span><span class="sxs-lookup"><span data-stu-id="c8504-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="c8504-228">**Agente** e **Admin** contas precisam toobe provisionada manualmente no **Zendesk** antes de entrar.</span><span class="sxs-lookup"><span data-stu-id="c8504-228">**Agent** and **Admin** accounts need toobe manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="c8504-229">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c8504-229">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8504-230">Faça logon no tooyour **Zendesk** locatário.</span><span class="sxs-lookup"><span data-stu-id="c8504-230">Log in tooyour **Zendesk** tenant.</span></span>

2. <span data-ttu-id="c8504-231">Selecione Olá **lista de clientes** guia.</span><span class="sxs-lookup"><span data-stu-id="c8504-231">Select hello **Customer List** tab.</span></span>

3. <span data-ttu-id="c8504-232">Selecione Olá **usuário** guia e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c8504-232">Select hello **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="c8504-233">![Adicionar Usuário](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="c8504-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="c8504-234">Digite o endereço de email de saudação de uma conta existente do AD do Azure você deseja tooprovision e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="c8504-234">Type hello email address of an existing Azure AD account you want tooprovision, and then click **Save**.</span></span>
   
    <span data-ttu-id="c8504-235">![Novo Usuário](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="c8504-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="c8504-236">Você pode usar qualquer ferramenta de criação outros Zendesk usuário conta ou APIs fornecidas pelo Zendesk tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="c8504-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk tooprovision AAD user accounts.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c8504-237">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8504-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c8504-238">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooZendesk.</span><span class="sxs-lookup"><span data-stu-id="c8504-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZendesk.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c8504-240">**tooassign Britta Simon tooZendesk, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c8504-240">**tooassign Britta Simon tooZendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8504-241">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c8504-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c8504-243">Na lista de aplicativos hello, selecione **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="c8504-243">In hello applications list, select **Zendesk**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="c8504-245">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c8504-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c8504-247">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c8504-247">Click **Add** button.</span></span> <span data-ttu-id="c8504-248">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8504-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c8504-250">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8504-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c8504-251">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8504-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c8504-252">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8504-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c8504-253">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c8504-253">Testing single sign-on</span></span>

<span data-ttu-id="c8504-254">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8504-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c8504-255">Quando você clica em bloco Zendesk Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Zendesk aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c8504-255">When you click hello Zendesk tile in hello Access Panel, you should get automatically signed-on tooyour Zendesk application.</span></span>
<span data-ttu-id="c8504-256">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8504-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c8504-257">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c8504-257">Additional resources</span></span>

* [<span data-ttu-id="c8504-258">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c8504-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c8504-259">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c8504-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
