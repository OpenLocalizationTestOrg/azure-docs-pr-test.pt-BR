---
title: "Tutorial: Integração do Azure Active Directory ao Freshservice | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Freshservice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d73624b87d058f66885ae72fda69a0aacc89c1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="c2bcf-103">Tutorial: Integração do Azure Active Directory ao FreshService</span><span class="sxs-lookup"><span data-stu-id="c2bcf-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="c2bcf-104">Neste tutorial, você aprenderá como toointegrate Freshservice com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c2bcf-104">In this tutorial, you learn how toointegrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c2bcf-105">Integrando o Freshservice com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2bcf-105">Integrating Freshservice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c2bcf-106">Você pode controlar no AD do Azure que tenha acesso tooFreshservice</span><span class="sxs-lookup"><span data-stu-id="c2bcf-106">You can control in Azure AD who has access tooFreshservice</span></span>
- <span data-ttu-id="c2bcf-107">Você pode habilitar seu usuários tooautomatically get conectado tooFreshservice (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c2bcf-107">You can enable your users tooautomatically get signed-on tooFreshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c2bcf-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c2bcf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c2bcf-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c2bcf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2bcf-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c2bcf-110">Prerequisites</span></span>

<span data-ttu-id="c2bcf-111">tooconfigure integração do AD do Azure com Freshservice, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2bcf-111">tooconfigure Azure AD integration with Freshservice, you need hello following items:</span></span>

- <span data-ttu-id="c2bcf-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c2bcf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c2bcf-113">Uma assinatura habilitada para logon único do Freshservice</span><span class="sxs-lookup"><span data-stu-id="c2bcf-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c2bcf-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c2bcf-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c2bcf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c2bcf-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c2bcf-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c2bcf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c2bcf-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c2bcf-118">Scenario description</span></span>
<span data-ttu-id="c2bcf-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c2bcf-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c2bcf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c2bcf-121">Adicionando Freshservice da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c2bcf-121">Adding Freshservice from hello gallery</span></span>
2. <span data-ttu-id="c2bcf-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c2bcf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-hello-gallery"></a><span data-ttu-id="c2bcf-123">Adicionando Freshservice da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c2bcf-123">Adding Freshservice from hello gallery</span></span>
<span data-ttu-id="c2bcf-124">integração de saudação tooconfigure do Freshservice no AD do Azure, você precisa tooadd Freshservice da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-124">tooconfigure hello integration of Freshservice into Azure AD, you need tooadd Freshservice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c2bcf-125">**tooadd Freshservice da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c2bcf-125">**tooadd Freshservice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2bcf-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c2bcf-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c2bcf-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c2bcf-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c2bcf-133">Na caixa de pesquisa hello, digite **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-133">In hello search box, type **Freshservice**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="c2bcf-135">No painel de resultados de saudação, selecione **Freshservice**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-135">In hello results panel, select **Freshservice**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c2bcf-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c2bcf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c2bcf-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Freshservice com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c2bcf-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Freshservice é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Freshservice is tooa user in Azure AD.</span></span> <span data-ttu-id="c2bcf-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Freshservice precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-140">In other words, a link relationship between an Azure AD user and hello related user in Freshservice needs toobe established.</span></span>

<span data-ttu-id="c2bcf-141">No Freshservice, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-141">In Freshservice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c2bcf-142">tooconfigure e teste de logon único do AD do Azure com Freshservice, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2bcf-142">tooconfigure and test Azure AD single sign-on with Freshservice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c2bcf-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c2bcf-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c2bcf-145">**[Criar um usuário de teste do Freshservice](#creating-a-freshservice-test-user)**  -toohave um equivalente do Britta Simon no Freshservice é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - toohave a counterpart of Britta Simon in Freshservice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c2bcf-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c2bcf-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c2bcf-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c2bcf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c2bcf-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Freshservice.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="c2bcf-150">**tooconfigure AD do Azure-logon único com Freshservice, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c2bcf-150">**tooconfigure Azure AD single sign-on with Freshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2bcf-151">Em Olá portal do Azure, Olá **Freshservice** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-151">In hello Azure portal, on hello **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c2bcf-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="c2bcf-155">Em Olá **Freshservice domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2bcf-155">On hello **Freshservice Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="c2bcf-157">a.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-157">a.</span></span> <span data-ttu-id="c2bcf-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="c2bcf-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="c2bcf-159">b.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-159">b.</span></span> <span data-ttu-id="c2bcf-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="c2bcf-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c2bcf-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-161">These values are not real.</span></span> <span data-ttu-id="c2bcf-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c2bcf-163">Entre em contato com [equipe de suporte do cliente Freshservice](https://support.freshservice.com/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-163">Contact [Freshservice Client support team](https://support.freshservice.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="c2bcf-164">Em Olá **o certificado de autenticação SAML** seção, copie **impressão digital** o valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-164">On hello **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="c2bcf-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c2bcf-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c2bcf-168">Em Olá **Freshservice configuração** seção, clique em **configurar Freshservice** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-168">On hello **Freshservice Configuration** section, click **Configure Freshservice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c2bcf-169">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="c2bcf-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="c2bcf-171">Em uma janela de navegador web diferente, faça logon no site da empresa Freshservice tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-171">In a different web browser window, log in tooyour Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="c2bcf-172">No menu de saudação na parte superior de saudação, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-172">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="c2bcf-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c2bcf-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="c2bcf-174">Em Olá **Portal do cliente**, clique em **segurança**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-174">In hello **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="c2bcf-175">![Segurança](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Segurança")</span><span class="sxs-lookup"><span data-stu-id="c2bcf-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="c2bcf-176">Em Olá **segurança** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2bcf-176">In hello **Security** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c2bcf-177">![Logon Único](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="c2bcf-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="c2bcf-178">a.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-178">a.</span></span> <span data-ttu-id="c2bcf-179">Ative o **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="c2bcf-180">b.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-180">b.</span></span> <span data-ttu-id="c2bcf-181">Selecione **SSO do SAML**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="c2bcf-182">c.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-182">c.</span></span> <span data-ttu-id="c2bcf-183">Em Olá **URL de logon** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-183">In hello **SAML Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c2bcf-184">d.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-184">d.</span></span> <span data-ttu-id="c2bcf-185">Em Olá **URL de Logout** caixa de texto valor Olá colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-185">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c2bcf-186">e.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-186">e.</span></span> <span data-ttu-id="c2bcf-187">Em **impressão digital do certificado de segurança** caixa de texto, colar Olá **impressão digital** o valor de certificado que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-187">In **Security Certificate Fingerprint** textbox, paste hello **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c2bcf-188">f.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-188">f.</span></span> <span data-ttu-id="c2bcf-189">Clique em **Salvar**</span><span class="sxs-lookup"><span data-stu-id="c2bcf-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="c2bcf-190">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c2bcf-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c2bcf-191">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c2bcf-192">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c2bcf-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c2bcf-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c2bcf-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="c2bcf-194">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c2bcf-196">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c2bcf-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2bcf-197">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c2bcf-199">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c2bcf-201">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c2bcf-203">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2bcf-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c2bcf-205">a.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-205">a.</span></span> <span data-ttu-id="c2bcf-206">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c2bcf-207">b.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-207">b.</span></span> <span data-ttu-id="c2bcf-208">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c2bcf-209">c.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-209">c.</span></span> <span data-ttu-id="c2bcf-210">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c2bcf-211">d.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-211">d.</span></span> <span data-ttu-id="c2bcf-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="c2bcf-213">Como criar um usuário de teste do Freshservice</span><span class="sxs-lookup"><span data-stu-id="c2bcf-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="c2bcf-214">tooenable AD do Azure usuários toolog em tooFreshService, eles devem ser provisionados no FreshService.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-214">tooenable Azure AD users toolog in tooFreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="c2bcf-215">No caso de saudação do FreshService, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-215">In hello case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="c2bcf-216">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c2bcf-216">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2bcf-217">Faça logon no tooyour **FreshService** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-217">Log in tooyour **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="c2bcf-218">No menu de saudação na parte superior de saudação, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-218">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="c2bcf-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c2bcf-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="c2bcf-220">Em Olá **gerenciamento de usuários** seção, clique em **solicitantes**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-220">In hello **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="c2bcf-221">![Solicitantes](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Solicitantes")</span><span class="sxs-lookup"><span data-stu-id="c2bcf-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="c2bcf-222">Clique em **Novo Solicitante**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="c2bcf-223">![Novos Solicitantes](./media/active-directory-saas-freshservice-tutorial/ic790819.png "Novos Solicitantes")</span><span class="sxs-lookup"><span data-stu-id="c2bcf-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="c2bcf-224">Em Olá **novo solicitante** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c2bcf-224">In hello **New Requester** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c2bcf-225">![Novo Solicitante](./media/active-directory-saas-freshservice-tutorial/ic790820.png "Novo Solicitante")</span><span class="sxs-lookup"><span data-stu-id="c2bcf-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="c2bcf-226">a.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-226">a.</span></span> <span data-ttu-id="c2bcf-227">Digite hello **nome** e **Email** atributos de uma conta válida do Active Directory do Azure você deseja tooprovision em Olá relacionados caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-227">Enter hello **First Name** and **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="c2bcf-228">b.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-228">b.</span></span> <span data-ttu-id="c2bcf-229">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="c2bcf-230">proprietário de conta do Active Directory do Azure Olá obtém um email com uma conta de saudação do link tooconfirm antes de se tornar ativa</span><span class="sxs-lookup"><span data-stu-id="c2bcf-230">hello Azure Active Directory account holder gets an email including a link tooconfirm hello account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="c2bcf-231">Você pode usar qualquer ferramenta de criação outros FreshService usuário conta ou APIs fornecidas pelo FreshService tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-231">You can use any other FreshService user account creation tools or APIs provided by FreshService tooprovision AAD user accounts.</span></span>
>  

![Atribuir usuário][200] 

<span data-ttu-id="c2bcf-233">**tooassign Britta Simon tooFreshservice, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c2bcf-233">**tooassign Britta Simon tooFreshservice, perform hello following steps:**</span></span>

1. <span data-ttu-id="c2bcf-234">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c2bcf-236">Na lista de aplicativos hello, selecione **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-236">In hello applications list, select **Freshservice**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="c2bcf-238">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c2bcf-240">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-240">Click **Add** button.</span></span> <span data-ttu-id="c2bcf-241">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c2bcf-243">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c2bcf-244">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c2bcf-245">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c2bcf-246">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c2bcf-246">Testing single sign-on</span></span>

<span data-ttu-id="c2bcf-247">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c2bcf-248">Quando você clica em bloco Freshservice Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Freshservice aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c2bcf-248">When you click hello Freshservice tile in hello Access Panel, you should get automatically signed-on tooyour Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c2bcf-249">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c2bcf-249">Additional resources</span></span>

* [<span data-ttu-id="c2bcf-250">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c2bcf-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c2bcf-251">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c2bcf-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

