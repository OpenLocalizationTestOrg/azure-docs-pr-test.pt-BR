---
title: "Tutorial: integração do Azure Active Directory com o Zscaler ZSCloud | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Zscaler ZSCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: af6d5c1994e715cccf959cc9fd3ba998e5b9effa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="edc10-103">Tutorial: integração do Azure Active Directory com o Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="edc10-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="edc10-104">Neste tutorial, você aprenderá como toointegrate Zscaler ZSCloud com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="edc10-104">In this tutorial, you learn how toointegrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="edc10-105">Integrando o Zscaler ZSCloud com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="edc10-105">Integrating Zscaler ZSCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="edc10-106">Você pode controlar no AD do Azure que tenha acesso tooZscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="edc10-106">You can control in Azure AD who has access tooZscaler ZSCloud</span></span>
- <span data-ttu-id="edc10-107">Você pode habilitar seu usuários tooautomatically get conectado tooZscaler ZSCloud (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="edc10-107">You can enable your users tooautomatically get signed-on tooZscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="edc10-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="edc10-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="edc10-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="edc10-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edc10-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="edc10-110">Prerequisites</span></span>

<span data-ttu-id="edc10-111">tooconfigure integração do AD do Azure com o Zscaler ZSCloud, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="edc10-111">tooconfigure Azure AD integration with Zscaler ZSCloud, you need hello following items:</span></span>

- <span data-ttu-id="edc10-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="edc10-112">An Azure AD subscription</span></span>
- <span data-ttu-id="edc10-113">Uma assinatura habilitada para logon único do Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="edc10-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="edc10-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="edc10-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="edc10-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="edc10-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="edc10-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="edc10-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="edc10-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="edc10-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="edc10-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="edc10-118">Scenario description</span></span>
<span data-ttu-id="edc10-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="edc10-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="edc10-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="edc10-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="edc10-121">Adicionando Zscaler ZSCloud da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="edc10-121">Adding Zscaler ZSCloud from hello gallery</span></span>
2. <span data-ttu-id="edc10-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="edc10-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-hello-gallery"></a><span data-ttu-id="edc10-123">Adicionando Zscaler ZSCloud da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="edc10-123">Adding Zscaler ZSCloud from hello gallery</span></span>
<span data-ttu-id="edc10-124">integração de saudação tooconfigure do Zscaler ZSCloud no AD do Azure, você precisa tooadd Zscaler ZSCloud na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="edc10-124">tooconfigure hello integration of Zscaler ZSCloud into Azure AD, you need tooadd Zscaler ZSCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="edc10-125">**tooadd Zscaler ZSCloud da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="edc10-125">**tooadd Zscaler ZSCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="edc10-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="edc10-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="edc10-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="edc10-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="edc10-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="edc10-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="edc10-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edc10-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="edc10-133">Na caixa de pesquisa hello, digite **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="edc10-133">In hello search box, type **Zscaler ZSCloud**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="edc10-135">No painel de resultados de saudação, selecione **Zscaler ZSCloud**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="edc10-135">In hello results panel, select **Zscaler ZSCloud**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="edc10-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="edc10-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="edc10-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Zscaler ZSCloud, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="edc10-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="edc10-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Zscaler ZSCloud é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="edc10-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler ZSCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="edc10-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Zscaler ZSCloud precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="edc10-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler ZSCloud needs toobe established.</span></span>

<span data-ttu-id="edc10-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="edc10-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="edc10-142">tooconfigure e teste de logon único do AD do Azure com o Zscaler ZSCloud, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="edc10-142">tooconfigure and test Azure AD single sign-on with Zscaler ZSCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="edc10-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="edc10-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="edc10-144">**[Definir configurações de proxy](#configuring-proxy-settings)**  -configurações de proxy de saudação tooconfigure no Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="edc10-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="edc10-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="edc10-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="edc10-146">**[Criar um usuário de teste do Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)**  -toohave um equivalente do Britta Simon no Zscaler ZSCloud é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="edc10-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - toohave a counterpart of Britta Simon in Zscaler ZSCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="edc10-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="edc10-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="edc10-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="edc10-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="edc10-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="edc10-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="edc10-150">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="edc10-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="edc10-151">**tooconfigure AD do Azure-logon único com o Zscaler ZSCloud, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="edc10-151">**tooconfigure Azure AD single sign-on with Zscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="edc10-152">Em Olá portal do Azure, Olá **Zscaler ZSCloud** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="edc10-152">In hello Azure portal, on hello **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="edc10-154">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="edc10-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="edc10-156">Em Olá **Zscaler ZSCloud domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="edc10-156">On hello **Zscaler ZSCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="edc10-158">Em Olá **URL de logon** caixa de texto, digite a URL Olá usada por seu usuários em toosign tooyour aplicativo ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="edc10-158">In hello **Sign-on URL** textbox, type hello URL used by your users toosign-on tooyour ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="edc10-159">Você tem tooupdate esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="edc10-159">You have tooupdate this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="edc10-160">Entre em contato com [equipe de suporte do Zscaler ZSCloud cliente](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="edc10-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) tooget this value.</span></span> 
 
4. <span data-ttu-id="edc10-161">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="edc10-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="edc10-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="edc10-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="edc10-165">Em Olá **Zscaler ZSCloud configuração** seção, clique em **configurar Zscaler ZSCloud** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="edc10-165">On hello **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="edc10-166">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="edc10-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="edc10-168">Em uma janela do navegador web diferente, faça logon no tooyour site da empresa ZScaler ZSCloud como um administrador.</span><span class="sxs-lookup"><span data-stu-id="edc10-168">In a different web browser window, log in tooyour ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="edc10-169">No menu de saudação na parte superior de saudação, clique em **administração**.</span><span class="sxs-lookup"><span data-stu-id="edc10-169">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="edc10-170">![Administração](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="edc10-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="edc10-171">Em **Gerenciar Administradores e Funções**, clique em **Gerenciar Usuários e Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="edc10-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="edc10-172">![Gerenciar usuários e autenticação](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Gerenciar usuários e autenticação")</span><span class="sxs-lookup"><span data-stu-id="edc10-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="edc10-173">Em Olá **escolher opções de autenticação para sua organização** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="edc10-173">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="edc10-174">![Autenticação](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Autenticação")</span><span class="sxs-lookup"><span data-stu-id="edc10-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="edc10-175">a.</span><span class="sxs-lookup"><span data-stu-id="edc10-175">a.</span></span> <span data-ttu-id="edc10-176">Selecione **Autenticar usando o Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="edc10-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="edc10-177">b.</span><span class="sxs-lookup"><span data-stu-id="edc10-177">b.</span></span> <span data-ttu-id="edc10-178">Clique em **Configurar Parâmetros de Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="edc10-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="edc10-179">Em Olá **configurar parâmetros único do SAML logon** página de diálogo Executar Olá etapas a seguir e, em seguida, clique em **feito**</span><span class="sxs-lookup"><span data-stu-id="edc10-179">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="edc10-180">![Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="edc10-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="edc10-181">a.</span><span class="sxs-lookup"><span data-stu-id="edc10-181">a.</span></span> <span data-ttu-id="edc10-182">Saudação de colar **Single Sign-On URL do serviço SAML** valor em Olá **URL de usuários de toowhich do Portal SAML Olá são enviados para autenticação** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="edc10-182">Paste hello **SAML Single Sign-On Service URL** value into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="edc10-183">b.</span><span class="sxs-lookup"><span data-stu-id="edc10-183">b.</span></span> <span data-ttu-id="edc10-184">Em Olá **atributo que contém o nome de logon** caixa de texto, tipo **NameID**.</span><span class="sxs-lookup"><span data-stu-id="edc10-184">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="edc10-185">c.</span><span class="sxs-lookup"><span data-stu-id="edc10-185">c.</span></span> <span data-ttu-id="edc10-186">tooupload seu certificado baixado, clique em **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="edc10-186">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="edc10-187">d.</span><span class="sxs-lookup"><span data-stu-id="edc10-187">d.</span></span> <span data-ttu-id="edc10-188">Selecione **Habilitar Provisionamento Automático do SAML**.</span><span class="sxs-lookup"><span data-stu-id="edc10-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="edc10-189">Em Olá **configurar autenticação de usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="edc10-189">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="edc10-190">![Administração](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="edc10-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="edc10-191">a.</span><span class="sxs-lookup"><span data-stu-id="edc10-191">a.</span></span> <span data-ttu-id="edc10-192">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="edc10-192">Click **Save**.</span></span>

    <span data-ttu-id="edc10-193">b.</span><span class="sxs-lookup"><span data-stu-id="edc10-193">b.</span></span> <span data-ttu-id="edc10-194">Clique em **Ativar Agora**.</span><span class="sxs-lookup"><span data-stu-id="edc10-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="edc10-195">Definindo as configurações de proxy</span><span class="sxs-lookup"><span data-stu-id="edc10-195">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="edc10-196">configurações de proxy de saudação tooconfigure no Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="edc10-196">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="edc10-197">Inicie o **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="edc10-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="edc10-198">Selecione **opções da Internet** de saudação **ferramentas** menu para abrir Olá **opções da Internet** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edc10-198">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="edc10-199">![Opções da Internet](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Opções da Internet")</span><span class="sxs-lookup"><span data-stu-id="edc10-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="edc10-200">Clique em Olá **conexões** guia.</span><span class="sxs-lookup"><span data-stu-id="edc10-200">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="edc10-201">![Conexões](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Conexões")</span><span class="sxs-lookup"><span data-stu-id="edc10-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="edc10-202">Clique em **configurações da LAN** tooopen Olá **configurações da LAN** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edc10-202">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="edc10-203">Olá seção do servidor Proxy, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="edc10-203">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="edc10-204">![Servidor proxy](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Servidor proxy")</span><span class="sxs-lookup"><span data-stu-id="edc10-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="edc10-205">a.</span><span class="sxs-lookup"><span data-stu-id="edc10-205">a.</span></span> <span data-ttu-id="edc10-206">Selecione **Usar um servidor proxy para LAN**.</span><span class="sxs-lookup"><span data-stu-id="edc10-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="edc10-207">b.</span><span class="sxs-lookup"><span data-stu-id="edc10-207">b.</span></span> <span data-ttu-id="edc10-208">Na caixa de texto de endereço hello, digite **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="edc10-208">In hello Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="edc10-209">c.</span><span class="sxs-lookup"><span data-stu-id="edc10-209">c.</span></span> <span data-ttu-id="edc10-210">Na caixa de texto de porta hello, digite **80**.</span><span class="sxs-lookup"><span data-stu-id="edc10-210">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="edc10-211">d.</span><span class="sxs-lookup"><span data-stu-id="edc10-211">d.</span></span> <span data-ttu-id="edc10-212">Selecione **Ignorar servidor proxy para endereços locais**.</span><span class="sxs-lookup"><span data-stu-id="edc10-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="edc10-213">e.</span><span class="sxs-lookup"><span data-stu-id="edc10-213">e.</span></span> <span data-ttu-id="edc10-214">Clique em **Okey** tooclose Olá **configurações de rede Local (LAN)** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edc10-214">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="edc10-215">Clique em **Okey** tooclose Olá **opções da Internet** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edc10-215">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="edc10-216">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="edc10-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="edc10-217">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="edc10-217">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="edc10-219">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="edc10-219">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="edc10-220">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="edc10-220">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="edc10-222">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="edc10-222">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="edc10-224">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="edc10-224">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="edc10-226">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="edc10-226">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="edc10-228">a.</span><span class="sxs-lookup"><span data-stu-id="edc10-228">a.</span></span> <span data-ttu-id="edc10-229">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="edc10-229">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="edc10-230">b.</span><span class="sxs-lookup"><span data-stu-id="edc10-230">b.</span></span> <span data-ttu-id="edc10-231">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="edc10-231">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="edc10-232">c.</span><span class="sxs-lookup"><span data-stu-id="edc10-232">c.</span></span> <span data-ttu-id="edc10-233">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="edc10-233">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="edc10-234">d.</span><span class="sxs-lookup"><span data-stu-id="edc10-234">d.</span></span> <span data-ttu-id="edc10-235">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="edc10-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="edc10-236">Criar um usuário de teste do Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="edc10-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="edc10-237">toolog de usuários do AD do Azure de tooenable tooZScaler ZSCloud, elas devem ser provisionado tooZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="edc10-237">tooenable Azure AD users toolog in tooZScaler ZSCloud, they must be provisioned tooZScaler ZSCloud.</span></span>  
<span data-ttu-id="edc10-238">No caso de saudação do ZScaler ZSCloud, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="edc10-238">In hello case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="edc10-239">tooconfigure provisionamento de usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="edc10-239">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="edc10-240">Faça logon no tooyour **Zscaler** locatário.</span><span class="sxs-lookup"><span data-stu-id="edc10-240">Log in tooyour **Zscaler** tenant.</span></span>

2. <span data-ttu-id="edc10-241">Clique em **Administração**.</span><span class="sxs-lookup"><span data-stu-id="edc10-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="edc10-242">![Administração](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="edc10-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="edc10-243">Clique em **Gerenciamento de Usuários**.</span><span class="sxs-lookup"><span data-stu-id="edc10-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="edc10-244">![Adicionar](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Adicionar")</span><span class="sxs-lookup"><span data-stu-id="edc10-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="edc10-245">Em Olá **usuários** , clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="edc10-245">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="edc10-246">![Adicionar](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Adicionar")</span><span class="sxs-lookup"><span data-stu-id="edc10-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="edc10-247">Na seção Adicionar usuário do hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="edc10-247">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="edc10-248">![Adicionar Usuário](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="edc10-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="edc10-249">a.</span><span class="sxs-lookup"><span data-stu-id="edc10-249">a.</span></span> <span data-ttu-id="edc10-250">Saudação de tipo **UserID**, **nome de exibição do usuário**, **senha**, **Confirmar senha**e, em seguida, selecione **grupos**e hello **departamento** de uma conta válida do AAD você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="edc10-250">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="edc10-251">b.</span><span class="sxs-lookup"><span data-stu-id="edc10-251">b.</span></span> <span data-ttu-id="edc10-252">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="edc10-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="edc10-253">Você pode usar qualquer ferramenta de criação outros ZScaler ZSCloud usuário conta ou APIs fornecidas pelo ZScaler ZSCloud tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="edc10-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="edc10-254">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="edc10-254">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="edc10-255">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooZscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="edc10-255">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler ZSCloud.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="edc10-257">**tooassign tooZscaler Britta Simon ZSCloud, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="edc10-257">**tooassign Britta Simon tooZscaler ZSCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="edc10-258">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="edc10-258">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="edc10-260">Na lista de aplicativos hello, selecione **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="edc10-260">In hello applications list, select **Zscaler ZSCloud**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="edc10-262">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="edc10-262">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="edc10-264">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="edc10-264">Click **Add** button.</span></span> <span data-ttu-id="edc10-265">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edc10-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="edc10-267">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="edc10-267">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="edc10-268">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edc10-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="edc10-269">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="edc10-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="edc10-270">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="edc10-270">Testing single sign-on</span></span>

<span data-ttu-id="edc10-271">Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="edc10-271">If you want tootest your single sign-on settings, open hello Access Panel.</span></span>

<span data-ttu-id="edc10-272">Quando você clica em Olá Zscaler ZSCloud lado a lado no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="edc10-272">When you click hello Zscaler ZSCloud tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler ZSCloud application.</span></span>

<span data-ttu-id="edc10-273">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="edc10-273">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="edc10-274">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="edc10-274">Additional resources</span></span>

* [<span data-ttu-id="edc10-275">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="edc10-275">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="edc10-276">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="edc10-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

