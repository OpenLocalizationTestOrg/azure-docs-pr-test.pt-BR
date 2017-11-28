---
title: "Tutorial: Integração do Azure Active Directory com o Adobe Sign | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Adobe sinal."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9385723-8fe7-4340-8afb-1508dac3e92b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: b4b07907f30a0890003554a02a76d968400b43ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adobe-sign"></a><span data-ttu-id="4c0d6-103">Tutorial: Integração do Azure Active Directory ao Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="4c0d6-103">Tutorial: Azure Active Directory integration with Adobe Sign</span></span>

<span data-ttu-id="4c0d6-104">Neste tutorial, você aprenderá como toointegrate Adobe entrar com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="4c0d6-104">In this tutorial, you learn how toointegrate Adobe Sign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4c0d6-105">Integração do Adobe sinal com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="4c0d6-105">Integrating Adobe Sign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4c0d6-106">Você pode controlar no AD do Azure que tenha acesso tooAdobe sinal</span><span class="sxs-lookup"><span data-stu-id="4c0d6-106">You can control in Azure AD who has access tooAdobe Sign</span></span>
- <span data-ttu-id="4c0d6-107">Você pode habilitar seu usuários tooautomatically get conectado tooAdobe logon (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c0d6-107">You can enable your users tooautomatically get signed-on tooAdobe Sign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4c0d6-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4c0d6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4c0d6-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4c0d6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c0d6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4c0d6-110">Prerequisites</span></span>

<span data-ttu-id="4c0d6-111">tooconfigure integração do AD do Azure com Adobe sinal, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="4c0d6-111">tooconfigure Azure AD integration with Adobe Sign, you need hello following items:</span></span>

- <span data-ttu-id="4c0d6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c0d6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4c0d6-113">Uma assinatura habilitada para logon único do Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="4c0d6-113">An Adobe Sign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4c0d6-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4c0d6-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4c0d6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4c0d6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4c0d6-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4c0d6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4c0d6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4c0d6-118">Scenario description</span></span>
<span data-ttu-id="4c0d6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4c0d6-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="4c0d6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4c0d6-121">Adicionando entrada Adobe da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4c0d6-121">Adding Adobe Sign from hello gallery</span></span>
2. <span data-ttu-id="4c0d6-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c0d6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adobe-sign-from-hello-gallery"></a><span data-ttu-id="4c0d6-123">Adicionando entrada Adobe da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4c0d6-123">Adding Adobe Sign from hello gallery</span></span>
<span data-ttu-id="4c0d6-124">integração de saudação tooconfigure do sinal do Adobe no AD do Azure, você precisa tooadd Adobe entrada na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-124">tooconfigure hello integration of Adobe Sign into Azure AD, you need tooadd Adobe Sign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4c0d6-125">**tooadd entrada Adobe da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4c0d6-125">**tooadd Adobe Sign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c0d6-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4c0d6-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4c0d6-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4c0d6-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4c0d6-133">Na caixa de pesquisa hello, digite **entrada Adobe**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-133">In hello search box, type **Adobe Sign**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_search.png)

5. <span data-ttu-id="4c0d6-135">No painel de resultados de saudação, selecione **entrada Adobe**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-135">In hello results panel, select **Adobe Sign**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4c0d6-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c0d6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4c0d6-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Adobe Sign, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-138">In this section, you configure and test Azure AD single sign-on with Adobe Sign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4c0d6-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na entrada Adobe é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Adobe Sign is tooa user in Azure AD.</span></span> <span data-ttu-id="4c0d6-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na entrada Adobe precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-140">In other words, a link relationship between an Azure AD user and hello related user in Adobe Sign needs toobe established.</span></span>

<span data-ttu-id="4c0d6-141">Na entrada do Adobe, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-141">In Adobe Sign, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4c0d6-142">tooconfigure e teste de logon único do AD do Azure com Adobe sinal, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="4c0d6-142">tooconfigure and test Azure AD single sign-on with Adobe Sign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4c0d6-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4c0d6-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4c0d6-145">**[Criar um usuário de teste de entrada Adobe](#creating-an-adobe-sign-test-user)**  -toohave um equivalente do Britta Simon no sinal de Adobe toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-145">**[Creating an Adobe Sign test user](#creating-an-adobe-sign-test-user)** - toohave a counterpart of Britta Simon in Adobe Sign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4c0d6-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4c0d6-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4c0d6-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c0d6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4c0d6-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de entrada do Adobe.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Adobe Sign application.</span></span>

<span data-ttu-id="4c0d6-150">**tooconfigure AD do Azure-logon único com o sinal do Adobe, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4c0d6-150">**tooconfigure Azure AD single sign-on with Adobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c0d6-151">Em Olá portal do Azure, Olá **entrada Adobe** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-151">In hello Azure portal, on hello **Adobe Sign** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4c0d6-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_samlbase.png)

3. <span data-ttu-id="4c0d6-155">Em Olá **URLs e domínio de logon do Adobe** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4c0d6-155">On hello **Adobe Sign Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_url.png)

    <span data-ttu-id="4c0d6-157">a.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-157">a.</span></span> <span data-ttu-id="4c0d6-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.echosign.com/`</span><span class="sxs-lookup"><span data-stu-id="4c0d6-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com/`</span></span>

    <span data-ttu-id="4c0d6-159">b.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-159">b.</span></span> <span data-ttu-id="4c0d6-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.echosign.com`</span><span class="sxs-lookup"><span data-stu-id="4c0d6-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.echosign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4c0d6-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-161">These values are not real.</span></span> <span data-ttu-id="4c0d6-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4c0d6-163">Entre em contato com [equipe de suporte de cliente de entrada Adobe](https://helpx.adobe.com/in/contact/support.html) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-163">Contact [Adobe Sign Client support team](https://helpx.adobe.com/in/contact/support.html) tooget these values.</span></span> 
 
4. <span data-ttu-id="4c0d6-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_certificate.png) 

5. <span data-ttu-id="4c0d6-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4c0d6-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4c0d6-168">Em Olá **configuração de entrada do Adobe** seção, clique em **configurar o logon do Adobe** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-168">On hello **Adobe Sign Configuration** section, click **Configure Adobe Sign** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4c0d6-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="4c0d6-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_configure.png) 


7. <span data-ttu-id="4c0d6-171">Em uma janela de navegador web diferente, faça logon no site da empresa tooyour Adobe logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-171">In a different web browser window, log in tooyour Adobe Sign company site as an administrator.</span></span>

8. <span data-ttu-id="4c0d6-172">No menu de saudação na parte superior de saudação, clique em **conta**e, em seguida, no painel de navegação Olá no lado esquerdo do hello, clique em **configurações SAML** em **configurações de conta**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-172">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **SAML Settings** under **Account Settings**.</span></span>
   
   <span data-ttu-id="4c0d6-173">![Conta](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Conta")</span><span class="sxs-lookup"><span data-stu-id="4c0d6-173">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789520.png "Account")</span></span>

9. <span data-ttu-id="4c0d6-174">Olá seção configurações do SAML, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4c0d6-174">In hello SAML Settings section, perform hello following steps:</span></span>
   
   <span data-ttu-id="4c0d6-175">![Configurações do SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "Configurações do SAML")</span><span class="sxs-lookup"><span data-stu-id="4c0d6-175">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789521.png "SAML Settings")</span></span>
   
   <span data-ttu-id="4c0d6-176">a.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-176">a.</span></span> <span data-ttu-id="4c0d6-177">Para **Modo do SAML**, selecione **SAML Obrigatório**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-177">As **SAML Mode**, select **SAML Mandatory**.</span></span>
   
   <span data-ttu-id="4c0d6-178">b.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-178">b.</span></span> <span data-ttu-id="4c0d6-179">Selecione **toolog permitem que os administradores usando suas credenciais do EchoSign**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-179">Select **Allow EchoSign Account Administrators toolog in using their EchoSign Credentials**.</span></span>
   
   <span data-ttu-id="4c0d6-180">c.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-180">c.</span></span> <span data-ttu-id="4c0d6-181">Para **Criação de Usuário**, selecione **Adicionar automaticamente os usuários autenticados por meio do SAML**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-181">As **User Creation**, select **Automatically add users authenticated through SAML**.</span></span>

10. <span data-ttu-id="4c0d6-182">Mova, executar Olá seguindo as etapas:</span><span class="sxs-lookup"><span data-stu-id="4c0d6-182">Move on, performing hello following steps:</span></span>

       <span data-ttu-id="4c0d6-183">![Configurações do SAML](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "Configurações do SAML")</span><span class="sxs-lookup"><span data-stu-id="4c0d6-183">![SAML Settings](./media/active-directory-saas-adobe-echosign-tutorial/ic789522.png "SAML Settings")</span></span>

    <span data-ttu-id="4c0d6-184">a.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-184">a.</span></span> <span data-ttu-id="4c0d6-185">Colar **ID da entidade SAML**, que você copiou do portal do Azure em Olá **ID da entidade IdP** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-185">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP Entity ID** textbox.</span></span>
    
    <span data-ttu-id="4c0d6-186">b.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-186">b.</span></span> <span data-ttu-id="4c0d6-187">Colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure em Olá **URL de logon IdP** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-187">Paste **SAML Single Sign-On Service URL**, which you have copied from Azure portal into hello **IdP Login URL** textbox.</span></span>
   
    <span data-ttu-id="4c0d6-188">c.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-188">c.</span></span> <span data-ttu-id="4c0d6-189">Colar **URL de logout**, que você copiou do portal do Azure em Olá **URL de Logout IdP** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-189">Paste **Sign-Out URL**, which you have copied from Azure portal into hello **IdP Logout URL** textbox.</span></span>

    <span data-ttu-id="4c0d6-190">d.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-190">d.</span></span> <span data-ttu-id="4c0d6-191">Abra seu baixado **Certificate(Base64)** no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **certificado IdP** caixa de texto</span><span class="sxs-lookup"><span data-stu-id="4c0d6-191">Open your downloaded **Certificate(Base64)** file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Certificate** textbox</span></span>

    <span data-ttu-id="4c0d6-192">e.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-192">e.</span></span> <span data-ttu-id="4c0d6-193">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-193">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="4c0d6-194">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="4c0d6-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4c0d6-195">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4c0d6-196">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4c0d6-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4c0d6-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c0d6-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="4c0d6-198">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4c0d6-200">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4c0d6-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c0d6-201">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4c0d6-203">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4c0d6-205">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4c0d6-207">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4c0d6-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-adobe-echosign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4c0d6-209">a.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-209">a.</span></span> <span data-ttu-id="4c0d6-210">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4c0d6-211">b.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-211">b.</span></span> <span data-ttu-id="4c0d6-212">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4c0d6-213">c.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-213">c.</span></span> <span data-ttu-id="4c0d6-214">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4c0d6-215">d.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-215">d.</span></span> <span data-ttu-id="4c0d6-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-216">Click **Create**.</span></span>
 
### <a name="creating-an-adobe-sign-test-user"></a><span data-ttu-id="4c0d6-217">Criando um usuário de teste do Adobe Sign</span><span class="sxs-lookup"><span data-stu-id="4c0d6-217">Creating an Adobe Sign test user</span></span>

<span data-ttu-id="4c0d6-218">tooenable AD do Azure usuários toolog em tooAdobe logon, eles devem ser provisionados no Adobe sinal.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-218">tooenable Azure AD users toolog in tooAdobe Sign, they must be provisioned into Adobe Sign.</span></span> <span data-ttu-id="4c0d6-219">No caso de saudação do Adobe sinal, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-219">In hello case of Adobe Sign, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="4c0d6-220">Você pode usar qualquer outra entrada Adobe usuário conta ferramenta de criação ou APIs fornecidas pelo Adobe sinal tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-220">You can use any other Adobe Sign user account creation tools or APIs provided by Adobe Sign tooprovision AAD user accounts.</span></span> 

<span data-ttu-id="4c0d6-221">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4c0d6-221">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c0d6-222">Faça logon no tooyour **entrada Adobe** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-222">Log in tooyour **Adobe Sign** company site as administrator.</span></span>

2. <span data-ttu-id="4c0d6-223">No menu de saudação na parte superior de saudação, clique em **conta**e, em seguida, no painel de navegação Olá no lado esquerdo do hello, clique em **usuários e grupos**e, em seguida, clique em **criar um novo usuário**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-223">In hello menu on hello top, click **Account**, and then, in hello navigation pane on hello left side, click **Users & Groups**, and then, click **Create a new user**.</span></span>
   
   <span data-ttu-id="4c0d6-224">![Conta](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Conta")</span><span class="sxs-lookup"><span data-stu-id="4c0d6-224">![Account](./media/active-directory-saas-adobe-echosign-tutorial/ic789524.png "Account")</span></span>
   
3. <span data-ttu-id="4c0d6-225">Em Olá **criar novo usuário** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4c0d6-225">In hello **Create New User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="4c0d6-226">![Criar usuário](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Criar usuário")</span><span class="sxs-lookup"><span data-stu-id="4c0d6-226">![Create User](./media/active-directory-saas-adobe-echosign-tutorial/ic789525.png "Create User")</span></span>
   
   <span data-ttu-id="4c0d6-227">a.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-227">a.</span></span> <span data-ttu-id="4c0d6-228">Saudação de tipo **endereço de Email**, **nome**, e **Sobrenome** de uma conta válida do AAD você deseja tooprovision em Olá relacionados caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-228">Type hello **Email Address**, **First Name**, and **Last Name** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="4c0d6-229">b.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-229">b.</span></span> <span data-ttu-id="4c0d6-230">Clique em **Criar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-230">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="4c0d6-231">proprietário de conta do Active Directory do Azure Olá recebe um email que inclui uma conta de saudação do link tooconfirm antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-231">hello Azure Active Directory account holder receives an email that includes a link tooconfirm hello account before it becomes active.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4c0d6-232">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4c0d6-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4c0d6-233">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooAdobe sinal.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAdobe Sign.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4c0d6-235">**tooassign Britta Simon tooAdobe sinal, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4c0d6-235">**tooassign Britta Simon tooAdobe Sign, perform hello following steps:**</span></span>

1. <span data-ttu-id="4c0d6-236">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4c0d6-238">Na lista de aplicativos hello, selecione **entrada Adobe**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-238">In hello applications list, select **Adobe Sign**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-adobe-echosign-tutorial/tutorial_adobesign_app.png) 

3. <span data-ttu-id="4c0d6-240">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4c0d6-242">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-242">Click **Add** button.</span></span> <span data-ttu-id="4c0d6-243">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4c0d6-245">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4c0d6-246">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4c0d6-247">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4c0d6-248">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4c0d6-248">Testing single sign-on</span></span>

<span data-ttu-id="4c0d6-249">Quando você clica em Olá entrada Adobe bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo de entrada do Adobe.</span><span class="sxs-lookup"><span data-stu-id="4c0d6-249">When you click hello Adobe Sign tile in hello Access Panel, you should get automatically signed-on tooyour Adobe Sign application.</span></span>
<span data-ttu-id="4c0d6-250">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4c0d6-250">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4c0d6-251">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4c0d6-251">Additional resources</span></span>

* [<span data-ttu-id="4c0d6-252">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4c0d6-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4c0d6-253">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4c0d6-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adobe-echosign-tutorial/tutorial_general_203.png

