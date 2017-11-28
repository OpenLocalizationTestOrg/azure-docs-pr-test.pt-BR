---
title: "Tutorial: integração do Azure Active Directory ao Expensify | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Expensify."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: 141513ef27c90dae2d77a52ecab2f89c4e5a55ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="d824a-103">Tutorial: integração do Azure Active Directory com o Expensify</span><span class="sxs-lookup"><span data-stu-id="d824a-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="d824a-104">Neste tutorial, você aprenderá como toointegrate Expensify com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="d824a-104">In this tutorial, you learn how toointegrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d824a-105">Integrando Expensify com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="d824a-105">Integrating Expensify with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d824a-106">Você pode controlar no AD do Azure que tenha acesso tooExpensify</span><span class="sxs-lookup"><span data-stu-id="d824a-106">You can control in Azure AD who has access tooExpensify</span></span>
- <span data-ttu-id="d824a-107">Você pode habilitar seu usuários tooautomatically get conectado tooExpensify (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d824a-107">You can enable your users tooautomatically get signed-on tooExpensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d824a-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d824a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d824a-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d824a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d824a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d824a-110">Prerequisites</span></span>

<span data-ttu-id="d824a-111">tooconfigure integração do AD do Azure com Expensify, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="d824a-111">tooconfigure Azure AD integration with Expensify, you need hello following items:</span></span>

- <span data-ttu-id="d824a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d824a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d824a-113">Uma assinatura habilitada para logon único do Expensify</span><span class="sxs-lookup"><span data-stu-id="d824a-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d824a-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d824a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d824a-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d824a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d824a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d824a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d824a-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d824a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d824a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d824a-118">Scenario description</span></span>
<span data-ttu-id="d824a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d824a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d824a-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="d824a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d824a-121">Adicionando Expensify da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d824a-121">Adding Expensify from hello gallery</span></span>
2. <span data-ttu-id="d824a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d824a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-hello-gallery"></a><span data-ttu-id="d824a-123">Adicionando Expensify da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d824a-123">Adding Expensify from hello gallery</span></span>
<span data-ttu-id="d824a-124">integração de saudação tooconfigure de Expensify no AD do Azure, você precisa tooadd Expensify da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d824a-124">tooconfigure hello integration of Expensify into Azure AD, you need tooadd Expensify from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d824a-125">**tooadd Expensify da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d824a-125">**tooadd Expensify from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d824a-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d824a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d824a-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d824a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d824a-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d824a-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="d824a-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d824a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="d824a-133">Na caixa de pesquisa hello, digite **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="d824a-133">In hello search box, type **Expensify**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="d824a-135">No painel de resultados de saudação, selecione **Expensify**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d824a-135">In hello results panel, select **Expensify**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d824a-137">configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d824a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d824a-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Expensify, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="d824a-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d824a-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Expensify é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d824a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Expensify is tooa user in Azure AD.</span></span> <span data-ttu-id="d824a-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Expensify precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="d824a-140">In other words, a link relationship between an Azure AD user and hello related user in Expensify needs toobe established.</span></span>

<span data-ttu-id="d824a-141">Expensify, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="d824a-141">In Expensify, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d824a-142">tooconfigure e teste de logon único do AD do Azure com Expensify, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="d824a-142">tooconfigure and test Azure AD single sign-on with Expensify, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d824a-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d824a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d824a-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d824a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d824a-145">**[Criar um usuário de teste Expensify](#creating-an-expensify-test-user)**  -toohave um equivalente do Britta Simon em Expensify é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="d824a-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - toohave a counterpart of Britta Simon in Expensify that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d824a-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="d824a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d824a-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="d824a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d824a-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d824a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d824a-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Expensify.</span><span class="sxs-lookup"><span data-stu-id="d824a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="d824a-150">**tooconfigure AD do Azure-logon único com Expensify, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d824a-150">**tooconfigure Azure AD single sign-on with Expensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="d824a-151">Em Olá portal do Azure, Olá **Expensify** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="d824a-151">In hello Azure portal, on hello **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="d824a-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="d824a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="d824a-155">Em Olá **Expensify domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d824a-155">On hello **Expensify Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="d824a-157">a.</span><span class="sxs-lookup"><span data-stu-id="d824a-157">a.</span></span> <span data-ttu-id="d824a-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.expensify.com/authentication/saml/login`</span><span class="sxs-lookup"><span data-stu-id="d824a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="d824a-159">b.</span><span class="sxs-lookup"><span data-stu-id="d824a-159">b.</span></span> <span data-ttu-id="d824a-160">Em Olá **URL de identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="d824a-160">In hello **Identifier URL** textbox, type a URL using hello following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="d824a-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="d824a-161">These values are not real.</span></span> <span data-ttu-id="d824a-162">Atualize esses valores com a URL real Olá URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="d824a-162">Update these values with hello actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="d824a-163">Entre em contato com [equipe de suporte do cliente Expensify](mailto:help@expensify.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="d824a-163">Contact [Expensify Client support team](mailto:help@expensify.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="d824a-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d824a-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="d824a-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d824a-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d824a-168">tooenable SSO no Expensify, primeiro é necessário tooenable **domínio controle** no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d824a-168">tooenable SSO in Expensify, you first need tooenable **Domain Control** in hello application.</span></span> <span data-ttu-id="d824a-169">Você pode habilitar o controle de domínio de aplicativo hello Olá etapas listadas [aqui](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="d824a-169">You can enable Domain Control in hello application through hello steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="d824a-170">Para obter suporte adicional, trabalhe com a [equipe de suporte ao Cliente do Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="d824a-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="d824a-171">Depois que o Controle de Domínio estiver habilitado, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="d824a-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="d824a-173">a.</span><span class="sxs-lookup"><span data-stu-id="d824a-173">a.</span></span> <span data-ttu-id="d824a-174">Logon tooyour Expensify aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d824a-174">Sign on tooyour Expensify application.</span></span>
    
    <span data-ttu-id="d824a-175">b.</span><span class="sxs-lookup"><span data-stu-id="d824a-175">b.</span></span> <span data-ttu-id="d824a-176">Na barra de ferramentas de saudação na parte superior do hello, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="d824a-176">In hello toolbar on hello top, click **Admin**.</span></span>
    
    <span data-ttu-id="d824a-177">c.</span><span class="sxs-lookup"><span data-stu-id="d824a-177">c.</span></span> <span data-ttu-id="d824a-178">No painel esquerdo do hello, clique em **domínio**.</span><span class="sxs-lookup"><span data-stu-id="d824a-178">In hello left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="d824a-179">d.</span><span class="sxs-lookup"><span data-stu-id="d824a-179">d.</span></span> <span data-ttu-id="d824a-180">Clique no nome do domínio verificado.</span><span class="sxs-lookup"><span data-stu-id="d824a-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="d824a-181">e.</span><span class="sxs-lookup"><span data-stu-id="d824a-181">e.</span></span> <span data-ttu-id="d824a-182">No painel esquerdo do hello, clique em **SAML**e, em seguida, selecione **habilitado**.</span><span class="sxs-lookup"><span data-stu-id="d824a-182">In hello left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="d824a-183">f.</span><span class="sxs-lookup"><span data-stu-id="d824a-183">f.</span></span> <span data-ttu-id="d824a-184">Abra hello baixado de metadados de Federação do AD do Azure no bloco de notas, Olá de cópia de conteúdo e, em seguida, cole-o em Olá **metadados do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="d824a-184">Open hello downloaded Federation Metadata from Azure AD in notepad, copy hello content, and then paste it into hello **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="d824a-185">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="d824a-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d824a-186">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="d824a-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d824a-187">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d824a-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d824a-188">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d824a-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="d824a-189">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d824a-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="d824a-191">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d824a-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d824a-192">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d824a-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d824a-194">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="d824a-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d824a-196">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d824a-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d824a-198">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d824a-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d824a-200">a.</span><span class="sxs-lookup"><span data-stu-id="d824a-200">a.</span></span> <span data-ttu-id="d824a-201">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d824a-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d824a-202">b.</span><span class="sxs-lookup"><span data-stu-id="d824a-202">b.</span></span> <span data-ttu-id="d824a-203">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d824a-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d824a-204">c.</span><span class="sxs-lookup"><span data-stu-id="d824a-204">c.</span></span> <span data-ttu-id="d824a-205">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="d824a-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d824a-206">d.</span><span class="sxs-lookup"><span data-stu-id="d824a-206">d.</span></span> <span data-ttu-id="d824a-207">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d824a-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="d824a-208">Criando um usuário de teste do Expensify</span><span class="sxs-lookup"><span data-stu-id="d824a-208">Creating an Expensify test user</span></span>

<span data-ttu-id="d824a-209">Nesta seção, você criará um usuário chamado Brenda Fernandes no Expensify.</span><span class="sxs-lookup"><span data-stu-id="d824a-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="d824a-210">Trabalhar com [equipe de suporte do cliente Expensify](mailto:help@expensify.com) tooadd usuários de saudação na plataforma de Expensify hello.</span><span class="sxs-lookup"><span data-stu-id="d824a-210">Work with [Expensify Client support team](mailto:help@expensify.com) tooadd hello users in hello Expensify platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d824a-211">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d824a-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d824a-212">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooExpensify.</span><span class="sxs-lookup"><span data-stu-id="d824a-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooExpensify.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="d824a-214">**tooassign Britta Simon tooExpensify, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d824a-214">**tooassign Britta Simon tooExpensify, perform hello following steps:**</span></span>

1. <span data-ttu-id="d824a-215">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d824a-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d824a-217">Na lista de aplicativos hello, selecione **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="d824a-217">In hello applications list, select **Expensify**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="d824a-219">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d824a-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="d824a-221">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d824a-221">Click **Add** button.</span></span> <span data-ttu-id="d824a-222">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d824a-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="d824a-224">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="d824a-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d824a-225">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d824a-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d824a-226">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d824a-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d824a-227">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="d824a-227">Testing single sign-on</span></span>

<span data-ttu-id="d824a-228">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d824a-228">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="d824a-229">Quando você clica em bloco Expensify Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Expensify aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d824a-229">When you click hello Expensify tile in hello Access Panel, you should get automatically signed-on tooyour Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d824a-230">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d824a-230">Additional resources</span></span>

* [<span data-ttu-id="d824a-231">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d824a-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d824a-232">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d824a-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

