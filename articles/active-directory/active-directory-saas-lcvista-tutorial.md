---
title: "Tutorial: Integração do Azure Active Directory ao LCVista | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e LCVista."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8db80d6e-3275-419f-aa39-6115a7bc9800
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: 5a4c7eb7d54b8b68c8241a97b9e516a3f6e55c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lcvista"></a><span data-ttu-id="87c1c-103">Tutorial: Integração do Azure Active Directory ao LCVista</span><span class="sxs-lookup"><span data-stu-id="87c1c-103">Tutorial: Azure Active Directory integration with LCVista</span></span>

<span data-ttu-id="87c1c-104">Neste tutorial, você aprenderá como toointegrate LCVista com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="87c1c-104">In this tutorial, you learn how toointegrate LCVista with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="87c1c-105">Integrando LCVista com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="87c1c-105">Integrating LCVista with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="87c1c-106">Você pode controlar no AD do Azure que tenha acesso tooLCVista</span><span class="sxs-lookup"><span data-stu-id="87c1c-106">You can control in Azure AD who has access tooLCVista</span></span>
- <span data-ttu-id="87c1c-107">Você pode habilitar seu usuários tooautomatically get conectado tooLCVista (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="87c1c-107">You can enable your users tooautomatically get signed-on tooLCVista (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="87c1c-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="87c1c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="87c1c-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="87c1c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="87c1c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="87c1c-110">Prerequisites</span></span>

<span data-ttu-id="87c1c-111">tooconfigure integração do AD do Azure com LCVista, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="87c1c-111">tooconfigure Azure AD integration with LCVista, you need hello following items:</span></span>

- <span data-ttu-id="87c1c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="87c1c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="87c1c-113">Uma assinatura habilitada para logon único do LCVista</span><span class="sxs-lookup"><span data-stu-id="87c1c-113">A LCVista single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="87c1c-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="87c1c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="87c1c-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="87c1c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="87c1c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="87c1c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="87c1c-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="87c1c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="87c1c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="87c1c-118">Scenario description</span></span>
<span data-ttu-id="87c1c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="87c1c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="87c1c-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="87c1c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="87c1c-121">Adicionando LCVista da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="87c1c-121">Adding LCVista from hello gallery</span></span>
2. <span data-ttu-id="87c1c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="87c1c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lcvista-from-hello-gallery"></a><span data-ttu-id="87c1c-123">Adicionando LCVista da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="87c1c-123">Adding LCVista from hello gallery</span></span>
<span data-ttu-id="87c1c-124">integração de saudação tooconfigure de LCVista no AD do Azure, você precisa tooadd LCVista da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="87c1c-124">tooconfigure hello integration of LCVista into Azure AD, you need tooadd LCVista from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="87c1c-125">**tooadd LCVista da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="87c1c-125">**tooadd LCVista from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="87c1c-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="87c1c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="87c1c-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="87c1c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="87c1c-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="87c1c-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="87c1c-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="87c1c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="87c1c-133">Na caixa de pesquisa hello, digite **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="87c1c-133">In hello search box, type **LCVista**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_search.png)

5. <span data-ttu-id="87c1c-135">No painel de resultados de saudação, selecione **LCVista**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="87c1c-135">In hello results panel, select **LCVista**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="87c1c-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="87c1c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="87c1c-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o LCVista, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="87c1c-138">In this section, you configure and test Azure AD single sign-on with LCVista based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="87c1c-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em LCVista é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="87c1c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LCVista is tooa user in Azure AD.</span></span> <span data-ttu-id="87c1c-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em LCVista precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="87c1c-140">In other words, a link relationship between an Azure AD user and hello related user in LCVista needs toobe established.</span></span>

<span data-ttu-id="87c1c-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em LCVista.</span><span class="sxs-lookup"><span data-stu-id="87c1c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LCVista.</span></span>

<span data-ttu-id="87c1c-142">tooconfigure e teste de logon único do AD do Azure com LCVista, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="87c1c-142">tooconfigure and test Azure AD single sign-on with LCVista, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="87c1c-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="87c1c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="87c1c-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="87c1c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="87c1c-145">**[Criar um usuário de teste LCVista](#creating-a-lcvista-test-user)**  -toohave um equivalente do Britta Simon em LCVista é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="87c1c-145">**[Creating a LCVista test user](#creating-a-lcvista-test-user)** - toohave a counterpart of Britta Simon in LCVista that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="87c1c-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="87c1c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="87c1c-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="87c1c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="87c1c-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="87c1c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="87c1c-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo LCVista.</span><span class="sxs-lookup"><span data-stu-id="87c1c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LCVista application.</span></span>

<span data-ttu-id="87c1c-150">**tooconfigure AD do Azure-logon único com LCVista, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="87c1c-150">**tooconfigure Azure AD single sign-on with LCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="87c1c-151">Em Olá portal do Azure, Olá **LCVista** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="87c1c-151">In hello Azure portal, on hello **LCVista** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="87c1c-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="87c1c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_samlbase.png)

3. <span data-ttu-id="87c1c-155">Em Olá **LCVista domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="87c1c-155">On hello **LCVista Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_url.png)

    <span data-ttu-id="87c1c-157">a.</span><span class="sxs-lookup"><span data-stu-id="87c1c-157">a.</span></span> <span data-ttu-id="87c1c-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.lcvista.com/rainier/login`</span><span class="sxs-lookup"><span data-stu-id="87c1c-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com/rainier/login`</span></span>

    <span data-ttu-id="87c1c-159">b.</span><span class="sxs-lookup"><span data-stu-id="87c1c-159">b.</span></span> <span data-ttu-id="87c1c-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.lcvista.com`</span><span class="sxs-lookup"><span data-stu-id="87c1c-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.lcvista.com`</span></span> 
     
    > [!NOTE] 
    > <span data-ttu-id="87c1c-161">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="87c1c-161">These values are not hello real.</span></span> <span data-ttu-id="87c1c-162">Atualizar esses valores com hello real identificador e URL de logon.</span><span class="sxs-lookup"><span data-stu-id="87c1c-162">Update these values with hello actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="87c1c-163">Entre em contato com [equipe de suporte do cliente LCVista](https://lcvista.com/contact) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="87c1c-163">Contact [LCVista Client support team](https://lcvista.com/contact) tooget these values.</span></span> 

4. <span data-ttu-id="87c1c-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="87c1c-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_certificate.png) 

5. <span data-ttu-id="87c1c-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="87c1c-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lcvista-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="87c1c-168">Em Olá **LCVista configuração** seção, clique em **configurar LCVista** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="87c1c-168">On hello **LCVista Configuration** section, click **Configure LCVista** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="87c1c-169">Saudação de cópia **ID da entidade SAML** e **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="87c1c-169">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_configure.png) 

7.  <span data-ttu-id="87c1c-171">Logon tooyour LCVista aplicativo como um administrador.</span><span class="sxs-lookup"><span data-stu-id="87c1c-171">Sign on tooyour LCVista application as an administrator.</span></span>

8. <span data-ttu-id="87c1c-172">Em Olá **configuração SAML** seção, verifique Olá **logon habilitar SAML** e insira os detalhes de saudação conforme mencionado na imagem.</span><span class="sxs-lookup"><span data-stu-id="87c1c-172">In hello **SAML Config** section, check hello **Enable SAML login** and enter hello details as mentioned in below image.</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_config.png)

    <span data-ttu-id="87c1c-174">a.</span><span class="sxs-lookup"><span data-stu-id="87c1c-174">a.</span></span> <span data-ttu-id="87c1c-175">Saudação de colar **URL do emissor** que você copiou do AD do Azure no hello **ID da entidade** seção.</span><span class="sxs-lookup"><span data-stu-id="87c1c-175">Paste hello **Issuer URL** which you have copied from Azure AD in hello **Entity ID** section.</span></span> 

    <span data-ttu-id="87c1c-176">b.</span><span class="sxs-lookup"><span data-stu-id="87c1c-176">b.</span></span> <span data-ttu-id="87c1c-177">Saudação de colar **o URL de serviço de logon único** que você copiou do AD do Azure no hello **URL** seção.</span><span class="sxs-lookup"><span data-stu-id="87c1c-177">Paste hello **Single Sign-On Service URL** which you have copied from Azure AD in hello **URL** section.</span></span>

    <span data-ttu-id="87c1c-178">c.</span><span class="sxs-lookup"><span data-stu-id="87c1c-178">c.</span></span> <span data-ttu-id="87c1c-179">De metadados (XML) que você baixou do portal do Azure, copie o valor de saudação **X509Certificate** e cole-o no hello **certificado x509** seção.</span><span class="sxs-lookup"><span data-stu-id="87c1c-179">From Metadata (XML) which you have downloaded from Azure portal, copy hello value **X509Certificate** and paste it in hello **x509 Certificate** section.</span></span>

    <span data-ttu-id="87c1c-180">d.</span><span class="sxs-lookup"><span data-stu-id="87c1c-180">d.</span></span> <span data-ttu-id="87c1c-181">Em Olá **atributo de nome** caixa de texto, colar Olá valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="87c1c-181">In hello **First name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>

    <span data-ttu-id="87c1c-182">e.</span><span class="sxs-lookup"><span data-stu-id="87c1c-182">e.</span></span> <span data-ttu-id="87c1c-183">Em Olá **atributo de Sobrenome** caixa de texto, colar Olá valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="87c1c-183">In hello **Last name attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>

    <span data-ttu-id="87c1c-184">f.</span><span class="sxs-lookup"><span data-stu-id="87c1c-184">f.</span></span> <span data-ttu-id="87c1c-185">Em Olá **atributo de Email** caixa de texto, colar Olá valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="87c1c-185">In hello **Email attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="87c1c-186">g.</span><span class="sxs-lookup"><span data-stu-id="87c1c-186">g.</span></span> <span data-ttu-id="87c1c-187">Em Olá **atributo Username** caixa de texto, colar Olá valor `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="87c1c-187">In hello **Username attribute** textbox, paste hello value `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>

    <span data-ttu-id="87c1c-188">e.</span><span class="sxs-lookup"><span data-stu-id="87c1c-188">e.</span></span> <span data-ttu-id="87c1c-189">Clique em **salvar** toosave configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="87c1c-189">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="87c1c-190">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="87c1c-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="87c1c-191">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="87c1c-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="87c1c-192">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="87c1c-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="87c1c-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="87c1c-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="87c1c-194">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="87c1c-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="87c1c-196">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="87c1c-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="87c1c-197">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="87c1c-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lcvista-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="87c1c-199">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="87c1c-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lcvista-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="87c1c-201">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="87c1c-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lcvista-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="87c1c-203">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="87c1c-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lcvista-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="87c1c-205">a.</span><span class="sxs-lookup"><span data-stu-id="87c1c-205">a.</span></span> <span data-ttu-id="87c1c-206">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="87c1c-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="87c1c-207">b.</span><span class="sxs-lookup"><span data-stu-id="87c1c-207">b.</span></span> <span data-ttu-id="87c1c-208">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="87c1c-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="87c1c-209">c.</span><span class="sxs-lookup"><span data-stu-id="87c1c-209">c.</span></span> <span data-ttu-id="87c1c-210">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="87c1c-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="87c1c-211">d.</span><span class="sxs-lookup"><span data-stu-id="87c1c-211">d.</span></span> <span data-ttu-id="87c1c-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="87c1c-212">Click **Create**.</span></span>
 
### <a name="creating-a-lcvista-test-user"></a><span data-ttu-id="87c1c-213">Criando um usuário de teste do LCVista</span><span class="sxs-lookup"><span data-stu-id="87c1c-213">Creating a LCVista test user</span></span>

<span data-ttu-id="87c1c-214">Nesta seção, você criará um usuário chamado Brenda Fernandes no LCVista.</span><span class="sxs-lookup"><span data-stu-id="87c1c-214">In this section, you create a user called Britta Simon in LCVista.</span></span> <span data-ttu-id="87c1c-215">Você precisa toocontact [equipe de suporte do cliente LCVista](https://lcvista.com/contact) tooadd usuários Olá Olá LCVista aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87c1c-215">You need toocontact [LCVista Client support team](https://lcvista.com/contact) tooadd hello users in hello LCVista application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="87c1c-216">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="87c1c-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="87c1c-217">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLCVista.</span><span class="sxs-lookup"><span data-stu-id="87c1c-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLCVista.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="87c1c-219">**tooassign Britta Simon tooLCVista, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="87c1c-219">**tooassign Britta Simon tooLCVista, perform hello following steps:**</span></span>

1. <span data-ttu-id="87c1c-220">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="87c1c-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="87c1c-222">Na lista de aplicativos hello, selecione **LCVista**.</span><span class="sxs-lookup"><span data-stu-id="87c1c-222">In hello applications list, select **LCVista**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lcvista-tutorial/tutorial_lcvista_app.png) 

3. <span data-ttu-id="87c1c-224">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="87c1c-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="87c1c-226">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="87c1c-226">Click **Add** button.</span></span> <span data-ttu-id="87c1c-227">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="87c1c-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="87c1c-229">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="87c1c-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="87c1c-230">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="87c1c-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="87c1c-231">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="87c1c-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="87c1c-232">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="87c1c-232">Testing single sign-on</span></span>

<span data-ttu-id="87c1c-233">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="87c1c-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span> <span data-ttu-id="87c1c-234">Clique em bloco de LCVista Olá Olá painel de acesso, você será redirecionado tooOrganization página de entrada.</span><span class="sxs-lookup"><span data-stu-id="87c1c-234">Click hello LCVista tile in hello Access Panel, you will be redirected tooOrganization sign on page.</span></span> <span data-ttu-id="87c1c-235">Após o logon bem-sucedido, você será conectado tooyour LCVista aplicativo.</span><span class="sxs-lookup"><span data-stu-id="87c1c-235">After successful login, you will be signed-on tooyour LCVista application.</span></span> <span data-ttu-id="87c1c-236">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="87c1c-236">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="87c1c-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="87c1c-237">Additional resources</span></span>

* [<span data-ttu-id="87c1c-238">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="87c1c-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="87c1c-239">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="87c1c-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lcvista-tutorial/tutorial_general_203.png

