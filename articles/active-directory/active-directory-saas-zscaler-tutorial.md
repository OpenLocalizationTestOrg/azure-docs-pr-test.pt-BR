---
title: "Tutorial: Integração do Azure Active Directory ao Zscaler | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Zscaler."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e2894534f5d6711fd6af618cd699fa5837b5bf26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a><span data-ttu-id="32929-103">Tutorial: Integração do Active Directory do Azure com o Zscaler</span><span class="sxs-lookup"><span data-stu-id="32929-103">Tutorial: Azure Active Directory integration with Zscaler</span></span>

<span data-ttu-id="32929-104">Neste tutorial, você aprenderá como toointegrate Zscaler com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="32929-104">In this tutorial, you learn how toointegrate Zscaler with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32929-105">Integrando o Zscaler com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="32929-105">Integrating Zscaler with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="32929-106">Você pode controlar no AD do Azure que tenha acesso tooZscaler</span><span class="sxs-lookup"><span data-stu-id="32929-106">You can control in Azure AD who has access tooZscaler</span></span>
- <span data-ttu-id="32929-107">Você pode habilitar seu usuários tooautomatically get conectado tooZscaler (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="32929-107">You can enable your users tooautomatically get signed-on tooZscaler (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32929-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="32929-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="32929-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32929-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32929-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="32929-110">Prerequisites</span></span>

<span data-ttu-id="32929-111">tooconfigure integração do AD do Azure com o Zscaler, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="32929-111">tooconfigure Azure AD integration with Zscaler, you need hello following items:</span></span>

- <span data-ttu-id="32929-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="32929-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32929-113">Uma assinatura do Zscaler habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="32929-113">A Zscaler single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32929-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="32929-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32929-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="32929-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32929-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="32929-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32929-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32929-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32929-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="32929-118">Scenario description</span></span>
<span data-ttu-id="32929-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="32929-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32929-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="32929-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32929-121">Adicionando Zscaler da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="32929-121">Adding Zscaler from hello gallery</span></span>
2. <span data-ttu-id="32929-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="32929-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-from-hello-gallery"></a><span data-ttu-id="32929-123">Adicionando Zscaler da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="32929-123">Adding Zscaler from hello gallery</span></span>
<span data-ttu-id="32929-124">integração de saudação tooconfigure do Zscaler no AD do Azure, você precisa tooadd Zscaler da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="32929-124">tooconfigure hello integration of Zscaler into Azure AD, you need tooadd Zscaler from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="32929-125">**tooadd Zscaler da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="32929-125">**tooadd Zscaler from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="32929-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="32929-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32929-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="32929-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="32929-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="32929-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="32929-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32929-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="32929-133">Na caixa de pesquisa hello, digite **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="32929-133">In hello search box, type **Zscaler**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_search.png)

5. <span data-ttu-id="32929-135">No painel de resultados de saudação, selecione **Zscaler**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="32929-135">In hello results panel, select **Zscaler**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32929-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="32929-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32929-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Zscaler com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="32929-138">In this section, you configure and test Azure AD single sign-on with Zscaler based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="32929-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Zscaler é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="32929-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler is tooa user in Azure AD.</span></span> <span data-ttu-id="32929-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Zscaler precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="32929-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler needs toobe established.</span></span>

<span data-ttu-id="32929-141">No Zscaler, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="32929-141">In Zscaler, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="32929-142">tooconfigure e teste de logon único do AD do Azure com o Zscaler, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="32929-142">tooconfigure and test Azure AD single sign-on with Zscaler, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="32929-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="32929-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="32929-144">**[Definir configurações de proxy](#configuring-proxy-settings)**  -configurações de proxy de saudação tooconfigure no Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="32929-144">**[Configuring proxy settings](#configuring-proxy-settings)** - tooconfigure hello proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="32929-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32929-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="32929-146">**[Criar um usuário de teste do Zscaler](#creating-a-zscaler-test-user)**  -toohave um equivalente do Britta Simon no Zscaler que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="32929-146">**[Creating a Zscaler test user](#creating-a-zscaler-test-user)** - toohave a counterpart of Britta Simon in Zscaler that is linked toohello Azure AD representation of user.</span></span>
5. <span data-ttu-id="32929-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="32929-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
6. <span data-ttu-id="32929-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="32929-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32929-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="32929-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32929-150">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Zscaler.</span><span class="sxs-lookup"><span data-stu-id="32929-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zscaler application.</span></span>

<span data-ttu-id="32929-151">**tooconfigure AD do Azure-logon único com o Zscaler, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="32929-151">**tooconfigure Azure AD single sign-on with Zscaler, perform hello following steps:**</span></span>

1. <span data-ttu-id="32929-152">Em Olá portal do Azure, Olá **Zscaler** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="32929-152">In hello Azure portal, on hello **Zscaler** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="32929-154">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="32929-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_samlbase.png)

3. <span data-ttu-id="32929-156">Em Olá **Zscaler domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="32929-156">On hello **Zscaler Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_url.png)

    <span data-ttu-id="32929-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.zsclaer.net`</span><span class="sxs-lookup"><span data-stu-id="32929-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.zsclaer.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32929-159">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="32929-159">This value is not real.</span></span> <span data-ttu-id="32929-160">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="32929-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="32929-161">Entre em contato com [equipe de suporte do Zscaler cliente](https://www.zscaler.com/company/contact) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="32929-161">Contact [Zscaler Client support team](https://www.zscaler.com/company/contact) tooget this value.</span></span> 

4. <span data-ttu-id="32929-162">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="32929-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_certificate.png) 

5. <span data-ttu-id="32929-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="32929-164">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32929-166">Em Olá **Zscaler configuração** seção, clique em **configurar Zscaler** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="32929-166">On hello **Zscaler Configuration** section, click **Configure Zscaler** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="32929-167">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="32929-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_configure.png) 

7. <span data-ttu-id="32929-169">Em uma janela de navegador web diferente, faça logon no site de empresa do ZScaler tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="32929-169">In a different web browser window, log in tooyour ZScaler company site as an administrator.</span></span>

8. <span data-ttu-id="32929-170">No menu de saudação na parte superior de saudação, clique em **administração**.</span><span class="sxs-lookup"><span data-stu-id="32929-170">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="32929-171">![Administração](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="32929-171">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="32929-172">Em **Gerenciar Administradores e Funções**, clique em **Gerenciar Usuários e Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="32929-172">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="32929-173">![Gerenciar usuários e autenticação](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Gerenciar usuários e autenticação")</span><span class="sxs-lookup"><span data-stu-id="32929-173">![Manage Users & Authentication](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="32929-174">Em Olá **escolher opções de autenticação para sua organização** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="32929-174">In hello **Choose Authentication Options for your Organization** section, perform hello following steps:</span></span>   
                
    <span data-ttu-id="32929-175">![Autenticação](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Autenticação")</span><span class="sxs-lookup"><span data-stu-id="32929-175">![Authentication](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="32929-176">a.</span><span class="sxs-lookup"><span data-stu-id="32929-176">a.</span></span> <span data-ttu-id="32929-177">Selecione **Autenticar usando o Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="32929-177">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="32929-178">b.</span><span class="sxs-lookup"><span data-stu-id="32929-178">b.</span></span> <span data-ttu-id="32929-179">Clique em **Configurar Parâmetros de Logon Único do SAML**.</span><span class="sxs-lookup"><span data-stu-id="32929-179">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="32929-180">Em Olá **configurar parâmetros único do SAML logon** página de diálogo Executar Olá etapas a seguir e, em seguida, clique em **feito**</span><span class="sxs-lookup"><span data-stu-id="32929-180">On hello **Configure SAML Single Sign-On Parameters** dialog page, perform hello following steps, and then click **Done**</span></span>

    <span data-ttu-id="32929-181">![Logon Único](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="32929-181">![Single Sign-On](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="32929-182">a.</span><span class="sxs-lookup"><span data-stu-id="32929-182">a.</span></span> <span data-ttu-id="32929-183">Saudação de colar **Single Sign-On URL do serviço SAML** valor que você copiou de saudação portal do Azure em hello **URL de usuários de toowhich do Portal SAML Olá são enviados para autenticação** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="32929-183">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **URL of hello SAML Portal toowhich users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="32929-184">b.</span><span class="sxs-lookup"><span data-stu-id="32929-184">b.</span></span> <span data-ttu-id="32929-185">Em Olá **atributo que contém o nome de logon** caixa de texto, tipo **NameID**.</span><span class="sxs-lookup"><span data-stu-id="32929-185">In hello **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="32929-186">c.</span><span class="sxs-lookup"><span data-stu-id="32929-186">c.</span></span> <span data-ttu-id="32929-187">tooupload seu certificado baixado, clique em **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="32929-187">tooupload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="32929-188">d.</span><span class="sxs-lookup"><span data-stu-id="32929-188">d.</span></span> <span data-ttu-id="32929-189">Selecione **Habilitar Provisionamento Automático do SAML**.</span><span class="sxs-lookup"><span data-stu-id="32929-189">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="32929-190">Em Olá **configurar autenticação de usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="32929-190">On hello **Configure User Authentication** dialog page, perform hello following steps:</span></span>

    <span data-ttu-id="32929-191">![Administração](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="32929-191">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="32929-192">a.</span><span class="sxs-lookup"><span data-stu-id="32929-192">a.</span></span> <span data-ttu-id="32929-193">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="32929-193">Click **Save**.</span></span>

    <span data-ttu-id="32929-194">b.</span><span class="sxs-lookup"><span data-stu-id="32929-194">b.</span></span> <span data-ttu-id="32929-195">Clique em **Ativar Agora**.</span><span class="sxs-lookup"><span data-stu-id="32929-195">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="32929-196">Definindo as configurações de proxy</span><span class="sxs-lookup"><span data-stu-id="32929-196">Configuring proxy settings</span></span>
### <a name="tooconfigure-hello-proxy-settings-in-internet-explorer"></a><span data-ttu-id="32929-197">configurações de proxy de saudação tooconfigure no Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="32929-197">tooconfigure hello proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="32929-198">Inicie o **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="32929-198">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="32929-199">Selecione **opções da Internet** de saudação **ferramentas** menu para abrir Olá **opções da Internet** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32929-199">Select **Internet options** from hello **Tools** menu for open hello **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="32929-200">![Opções da Internet](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Opções da Internet")</span><span class="sxs-lookup"><span data-stu-id="32929-200">![Internet Options](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="32929-201">Clique em Olá **conexões** guia.</span><span class="sxs-lookup"><span data-stu-id="32929-201">Click hello **Connections** tab.</span></span>   
  
     <span data-ttu-id="32929-202">![Conexões](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Conexões")</span><span class="sxs-lookup"><span data-stu-id="32929-202">![Connections](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="32929-203">Clique em **configurações da LAN** tooopen Olá **configurações da LAN** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32929-203">Click **LAN settings** tooopen hello **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="32929-204">Olá seção do servidor Proxy, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="32929-204">In hello Proxy server section, perform hello following steps:</span></span>   
   
    <span data-ttu-id="32929-205">![Servidor proxy](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Servidor proxy")</span><span class="sxs-lookup"><span data-stu-id="32929-205">![Proxy server](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="32929-206">a.</span><span class="sxs-lookup"><span data-stu-id="32929-206">a.</span></span> <span data-ttu-id="32929-207">Selecione **Usar um servidor proxy para LAN**.</span><span class="sxs-lookup"><span data-stu-id="32929-207">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="32929-208">b.</span><span class="sxs-lookup"><span data-stu-id="32929-208">b.</span></span> <span data-ttu-id="32929-209">Na caixa de texto de endereço hello, digite **gateway.zscaler.net**.</span><span class="sxs-lookup"><span data-stu-id="32929-209">In hello Address textbox, type **gateway.zscaler.net**.</span></span>

    <span data-ttu-id="32929-210">c.</span><span class="sxs-lookup"><span data-stu-id="32929-210">c.</span></span> <span data-ttu-id="32929-211">Na caixa de texto de porta hello, digite **80**.</span><span class="sxs-lookup"><span data-stu-id="32929-211">In hello Port textbox, type **80**.</span></span>

    <span data-ttu-id="32929-212">d.</span><span class="sxs-lookup"><span data-stu-id="32929-212">d.</span></span> <span data-ttu-id="32929-213">Selecione **Ignorar servidor proxy para endereços locais**.</span><span class="sxs-lookup"><span data-stu-id="32929-213">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="32929-214">e.</span><span class="sxs-lookup"><span data-stu-id="32929-214">e.</span></span> <span data-ttu-id="32929-215">Clique em **Okey** tooclose Olá **configurações de rede Local (LAN)** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32929-215">Click **OK** tooclose hello **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="32929-216">Clique em **Okey** tooclose Olá **opções da Internet** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32929-216">Click **OK** tooclose hello **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="32929-217">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="32929-217">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="32929-218">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="32929-218">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="32929-219">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="32929-219">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32929-220">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="32929-220">Creating an Azure AD test user</span></span>
<span data-ttu-id="32929-221">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="32929-221">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="32929-223">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="32929-223">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="32929-224">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="32929-224">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32929-226">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="32929-226">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32929-228">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="32929-228">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32929-230">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="32929-230">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-zscaler-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32929-232">a.</span><span class="sxs-lookup"><span data-stu-id="32929-232">a.</span></span> <span data-ttu-id="32929-233">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32929-233">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32929-234">b.</span><span class="sxs-lookup"><span data-stu-id="32929-234">b.</span></span> <span data-ttu-id="32929-235">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="32929-235">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32929-236">c.</span><span class="sxs-lookup"><span data-stu-id="32929-236">c.</span></span> <span data-ttu-id="32929-237">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="32929-237">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="32929-238">d.</span><span class="sxs-lookup"><span data-stu-id="32929-238">d.</span></span> <span data-ttu-id="32929-239">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="32929-239">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-test-user"></a><span data-ttu-id="32929-240">Criação de um usuário de teste do Zscaler</span><span class="sxs-lookup"><span data-stu-id="32929-240">Creating a Zscaler test user</span></span>

<span data-ttu-id="32929-241">toolog de usuários do AD do Azure de tooenable tooZScaler, elas devem ser provisionado tooZScaler.</span><span class="sxs-lookup"><span data-stu-id="32929-241">tooenable Azure AD users toolog in tooZScaler, they must be provisioned tooZScaler.</span></span>  
<span data-ttu-id="32929-242">No caso de saudação do ZScaler, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="32929-242">In hello case of ZScaler, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="32929-243">tooconfigure provisionamento de usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="32929-243">tooconfigure user provisioning, perform hello following steps:</span></span>

1. <span data-ttu-id="32929-244">Faça logon no tooyour **Zscaler** locatário.</span><span class="sxs-lookup"><span data-stu-id="32929-244">Log in tooyour **Zscaler** tenant.</span></span>

2. <span data-ttu-id="32929-245">Clique em **Administração**.</span><span class="sxs-lookup"><span data-stu-id="32929-245">Click **Administration**.</span></span>   
   
    <span data-ttu-id="32929-246">![Administração](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administração")</span><span class="sxs-lookup"><span data-stu-id="32929-246">![Administration](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="32929-247">Clique em **Gerenciamento de Usuários**.</span><span class="sxs-lookup"><span data-stu-id="32929-247">Click **User Management**.</span></span>   
        
     <span data-ttu-id="32929-248">![Adicionar](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Adicionar")</span><span class="sxs-lookup"><span data-stu-id="32929-248">![Add](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="32929-249">Em Olá **usuários** , clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="32929-249">In hello **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="32929-250">![Adicionar](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Adicionar")</span><span class="sxs-lookup"><span data-stu-id="32929-250">![Add](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="32929-251">Na seção Adicionar usuário do hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="32929-251">In hello Add User section, perform hello following steps:</span></span>
        
    <span data-ttu-id="32929-252">![Adicionar Usuário](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Adicionar Usuário")</span><span class="sxs-lookup"><span data-stu-id="32929-252">![Add User](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="32929-253">a.</span><span class="sxs-lookup"><span data-stu-id="32929-253">a.</span></span> <span data-ttu-id="32929-254">Saudação de tipo **UserID**, **nome de exibição do usuário**, **senha**, **Confirmar senha**e, em seguida, selecione **grupos**e hello **departamento** de uma conta válida do AAD você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="32929-254">Type hello **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and hello **Department** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="32929-255">b.</span><span class="sxs-lookup"><span data-stu-id="32929-255">b.</span></span> <span data-ttu-id="32929-256">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="32929-256">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="32929-257">Você pode usar qualquer ferramenta de criação outros ZScaler usuário conta ou APIs fornecidas pelo ZScaler tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="32929-257">You can use any other ZScaler user account creation tools or APIs provided by ZScaler tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="32929-258">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="32929-258">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="32929-259">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooZscaler.</span><span class="sxs-lookup"><span data-stu-id="32929-259">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZscaler.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="32929-261">**tooassign Britta Simon tooZscaler, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="32929-261">**tooassign Britta Simon tooZscaler, perform hello following steps:**</span></span>

1. <span data-ttu-id="32929-262">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="32929-262">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="32929-264">Na lista de aplicativos hello, selecione **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="32929-264">In hello applications list, select **Zscaler**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_app.png) 

3. <span data-ttu-id="32929-266">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="32929-266">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="32929-268">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="32929-268">Click **Add** button.</span></span> <span data-ttu-id="32929-269">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32929-269">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="32929-271">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="32929-271">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="32929-272">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32929-272">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32929-273">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="32929-273">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32929-274">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="32929-274">Testing single sign-on</span></span>

<span data-ttu-id="32929-275">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="32929-275">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="32929-276">Quando você clica em bloco Zscaler Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Zscaler aplicativo.</span><span class="sxs-lookup"><span data-stu-id="32929-276">When you click hello Zscaler tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler application.</span></span>
<span data-ttu-id="32929-277">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="32929-277">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="32929-278">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="32929-278">Additional resources</span></span>

* [<span data-ttu-id="32929-279">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="32929-279">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32929-280">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="32929-280">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_203.png

