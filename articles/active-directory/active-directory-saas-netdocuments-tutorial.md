---
title: "Tutorial: Integração do Azure Active Directory ao NetDocuments | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do NetDocuments."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1a47dc42-1a17-48a2-965e-eca4cfb2f197
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: ee9887553595a2492642aed4cb4abcd11d9cf599
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-netdocuments"></a><span data-ttu-id="c476f-103">Tutorial: Integração do Active Directory do Azure com o NetDocuments</span><span class="sxs-lookup"><span data-stu-id="c476f-103">Tutorial: Azure Active Directory integration with NetDocuments</span></span>

<span data-ttu-id="c476f-104">Neste tutorial, você aprenderá como toointegrate NetDocuments com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c476f-104">In this tutorial, you learn how toointegrate NetDocuments with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c476f-105">Integrando o NetDocuments com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c476f-105">Integrating NetDocuments with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c476f-106">Você pode controlar no AD do Azure que tenha acesso tooNetDocuments</span><span class="sxs-lookup"><span data-stu-id="c476f-106">You can control in Azure AD who has access tooNetDocuments</span></span>
- <span data-ttu-id="c476f-107">Você pode habilitar seus usuários tooautomatically get conectado tooNetDocuments (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c476f-107">You can enable your users tooautomatically get signed-on tooNetDocuments (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c476f-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c476f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c476f-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c476f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c476f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c476f-110">Prerequisites</span></span>

<span data-ttu-id="c476f-111">tooconfigure integração do AD do Azure com o NetDocuments, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c476f-111">tooconfigure Azure AD integration with NetDocuments, you need hello following items:</span></span>

- <span data-ttu-id="c476f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c476f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c476f-113">Uma assinatura habilitada para logon único do NetDocuments</span><span class="sxs-lookup"><span data-stu-id="c476f-113">A NetDocuments single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c476f-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c476f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c476f-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c476f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c476f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c476f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c476f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c476f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c476f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c476f-118">Scenario description</span></span>
<span data-ttu-id="c476f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c476f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c476f-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c476f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c476f-121">Adicionando NetDocuments da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c476f-121">Adding NetDocuments from hello gallery</span></span>
2. <span data-ttu-id="c476f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c476f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-netdocuments-from-hello-gallery"></a><span data-ttu-id="c476f-123">Adicionando NetDocuments da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c476f-123">Adding NetDocuments from hello gallery</span></span>
<span data-ttu-id="c476f-124">integração de saudação tooconfigure do NetDocuments no AD do Azure, você precisa tooadd NetDocuments da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c476f-124">tooconfigure hello integration of NetDocuments into Azure AD, you need tooadd NetDocuments from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c476f-125">**tooadd NetDocuments da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c476f-125">**tooadd NetDocuments from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c476f-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c476f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c476f-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c476f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c476f-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c476f-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c476f-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c476f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c476f-133">Na caixa de pesquisa hello, digite **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="c476f-133">In hello search box, type **NetDocuments**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_search.png)

5. <span data-ttu-id="c476f-135">No painel de resultados de saudação, selecione **NetDocuments**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c476f-135">In hello results panel, select **NetDocuments**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c476f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c476f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c476f-138">Nesta seção, você configurará e testará o logon único do Azure AD com o NetDocuments, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c476f-138">In this section, you configure and test Azure AD single sign-on with NetDocuments based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c476f-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no NetDocuments é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c476f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in NetDocuments is tooa user in Azure AD.</span></span> <span data-ttu-id="c476f-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no NetDocuments precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c476f-140">In other words, a link relationship between an Azure AD user and hello related user in NetDocuments needs toobe established.</span></span>

<span data-ttu-id="c476f-141">No NetDocuments, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c476f-141">In NetDocuments, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c476f-142">tooconfigure e teste de logon único do AD do Azure com o NetDocuments, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c476f-142">tooconfigure and test Azure AD single sign-on with NetDocuments, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c476f-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c476f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c476f-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c476f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c476f-145">**[Criar um usuário de teste do NetDocuments](#creating-a-netdocuments-test-user)**  -toohave um equivalente do Britta Simon no NetDocuments é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c476f-145">**[Creating a NetDocuments test user](#creating-a-netdocuments-test-user)** - toohave a counterpart of Britta Simon in NetDocuments that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c476f-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c476f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c476f-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c476f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c476f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c476f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c476f-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="c476f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your NetDocuments application.</span></span>

<span data-ttu-id="c476f-150">**tooconfigure AD do Azure-logon único com o NetDocuments, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c476f-150">**tooconfigure Azure AD single sign-on with NetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="c476f-151">Em Olá portal do Azure, Olá **NetDocuments** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c476f-151">In hello Azure portal, on hello **NetDocuments** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c476f-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c476f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_samlbase.png)

3. <span data-ttu-id="c476f-155">Em Olá **NetDocuments domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c476f-155">On hello **NetDocuments Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_url.png)

    <span data-ttu-id="c476f-157">a.</span><span class="sxs-lookup"><span data-stu-id="c476f-157">a.</span></span> <span data-ttu-id="c476f-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="c476f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    <span data-ttu-id="c476f-159">b.</span><span class="sxs-lookup"><span data-stu-id="c476f-159">b.</span></span> <span data-ttu-id="c476f-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span><span class="sxs-lookup"><span data-stu-id="c476f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://vault.netvoyage.com/neWeb2/docCent.aspx?whr=<user identifier>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c476f-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c476f-161">These values are not real.</span></span> <span data-ttu-id="c476f-162">Atualize esses valores com URL de logon real hello e a URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="c476f-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="c476f-163">Entre em contato com [equipe de suporte do NetDocuments](https://support.netdocuments.com/hc/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="c476f-163">Contact [NetDocuments support team](https://support.netdocuments.com/hc/) tooget these values.</span></span>
 
4. <span data-ttu-id="c476f-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c476f-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_certificate.png) 

5. <span data-ttu-id="c476f-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c476f-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netdocuments-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c476f-168">Em uma janela de navegador da Web diferente, faça logon no site de sua empresa do NetDocuments como administrador.</span><span class="sxs-lookup"><span data-stu-id="c476f-168">In a different web browser window, log into your NetDocuments company site as an administrator.</span></span>

7. <span data-ttu-id="c476f-169">Vá muito**Admin**.</span><span class="sxs-lookup"><span data-stu-id="c476f-169">Go too**Admin**.</span></span>

8. <span data-ttu-id="c476f-170">Clique em **Adicionar e remover usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c476f-170">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="c476f-171">![Repositório](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repositório")</span><span class="sxs-lookup"><span data-stu-id="c476f-171">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

9. <span data-ttu-id="c476f-172">Clique em **Configurar opções de autenticação avançadas**.</span><span class="sxs-lookup"><span data-stu-id="c476f-172">Click **Configure advanced authentication options**.</span></span>
    
    <span data-ttu-id="c476f-173">![Configurar opções de autenticação avançadas](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configurar opções de autenticação avançadas")</span><span class="sxs-lookup"><span data-stu-id="c476f-173">![Configure advanced authentication options](./media/active-directory-saas-netdocuments-tutorial/ic795048.png "Configure advanced authentication options")</span></span>

10. <span data-ttu-id="c476f-174">Em Olá **identidade federada** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c476f-174">On hello **Federated Identity** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="c476f-175">![Identidade Federada](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Identidade Federada")</span><span class="sxs-lookup"><span data-stu-id="c476f-175">![Federated Identitty](./media/active-directory-saas-netdocuments-tutorial/ic795049.png "Federated Identitty")</span></span>
   
    <span data-ttu-id="c476f-176">a.</span><span class="sxs-lookup"><span data-stu-id="c476f-176">a.</span></span> <span data-ttu-id="c476f-177">Para **Tipo de servidor de identidade federada**, selecione **Serviços de Federação do Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c476f-177">As **Federated identity server type**, select **Active Directory Federation Services**.</span></span>
   
    <span data-ttu-id="c476f-178">b.</span><span class="sxs-lookup"><span data-stu-id="c476f-178">b.</span></span> <span data-ttu-id="c476f-179">Clique em **Escolher arquivo**, Olá tooupload baixou o arquivo de metadados que você baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c476f-179">Click **Choose file**, tooupload hello downloaded metadata file which you have downloaded from Azure portal.</span></span>
   
    <span data-ttu-id="c476f-180">c.</span><span class="sxs-lookup"><span data-stu-id="c476f-180">c.</span></span> <span data-ttu-id="c476f-181">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c476f-181">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="c476f-182">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c476f-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c476f-183">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c476f-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c476f-184">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c476f-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c476f-185">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c476f-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="c476f-186">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c476f-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c476f-188">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c476f-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c476f-189">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c476f-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c476f-191">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c476f-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c476f-193">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c476f-193">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c476f-195">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c476f-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-netdocuments-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c476f-197">a.</span><span class="sxs-lookup"><span data-stu-id="c476f-197">a.</span></span> <span data-ttu-id="c476f-198">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c476f-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c476f-199">b.</span><span class="sxs-lookup"><span data-stu-id="c476f-199">b.</span></span> <span data-ttu-id="c476f-200">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c476f-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c476f-201">c.</span><span class="sxs-lookup"><span data-stu-id="c476f-201">c.</span></span> <span data-ttu-id="c476f-202">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c476f-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c476f-203">d.</span><span class="sxs-lookup"><span data-stu-id="c476f-203">d.</span></span> <span data-ttu-id="c476f-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c476f-204">Click **Create**.</span></span>
 
### <a name="creating-a-netdocuments-test-user"></a><span data-ttu-id="c476f-205">Criar um usuário de teste do NetDocuments</span><span class="sxs-lookup"><span data-stu-id="c476f-205">Creating a NetDocuments test user</span></span>

<span data-ttu-id="c476f-206">tooenable AD do Azure usuários toolog em tooNetDocuments, eles devem ser provisionados no NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="c476f-206">tooenable Azure AD users toolog in tooNetDocuments, they must be provisioned into NetDocuments.</span></span>  
<span data-ttu-id="c476f-207">No caso de saudação do NetDocuments, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="c476f-207">In hello case of NetDocuments, provisioning is a manual task.</span></span>

<span data-ttu-id="c476f-208">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c476f-208">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="c476f-209">Tocar em tooyour **NetDocuments** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="c476f-209">Sing on tooyour **NetDocuments** company site as administrator.</span></span>

2. <span data-ttu-id="c476f-210">No menu de saudação na parte superior de saudação, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="c476f-210">In hello menu on hello top, click **Admin**.</span></span>
   
    <span data-ttu-id="c476f-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c476f-211">![Admin](./media/active-directory-saas-netdocuments-tutorial/ic795051.png "Admin")</span></span>

3. <span data-ttu-id="c476f-212">Clique em **Adicionar e remover usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c476f-212">Click **Add and remove users and groups**.</span></span>
   
    <span data-ttu-id="c476f-213">![Repositório](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repositório")</span><span class="sxs-lookup"><span data-stu-id="c476f-213">![Repository](./media/active-directory-saas-netdocuments-tutorial/ic795047.png "Repository")</span></span>

4. <span data-ttu-id="c476f-214">Em Olá **endereço de Email** caixa de texto, digite o endereço de email de Olá de uma conta válida do Active Directory do Azure você deseja tooprovision e, em seguida, clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="c476f-214">In hello **Email Address** textbox, type hello email address of a valid Azure Active Directory account you want tooprovision, and then click **Add User**.</span></span>
   
    <span data-ttu-id="c476f-215">![Endereço de Email](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Endereço de Email")</span><span class="sxs-lookup"><span data-stu-id="c476f-215">![Email Address](./media/active-directory-saas-netdocuments-tutorial/ic795053.png "Email Address")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="c476f-216">proprietário de conta do Active Directory do Azure Olá receberá um email que inclui uma conta de saudação do link tooconfirm antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="c476f-216">hello Azure Active Directory account holder will get an email that includes a link tooconfirm hello account before it becomes active.</span></span> <span data-ttu-id="c476f-217">Você pode usar qualquer ferramenta de criação outros NetDocuments usuário conta ou APIs fornecidas pela NetDocuments tooprovision Azure Active Directory as contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="c476f-217">You can use any other NetDocuments user account creation tools or APIs provided by NetDocuments tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c476f-218">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c476f-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c476f-219">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooNetDocuments.</span><span class="sxs-lookup"><span data-stu-id="c476f-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNetDocuments.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c476f-221">**tooassign Britta Simon tooNetDocuments, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c476f-221">**tooassign Britta Simon tooNetDocuments, perform hello following steps:**</span></span>

1. <span data-ttu-id="c476f-222">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c476f-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c476f-224">Na lista de aplicativos hello, selecione **NetDocuments**.</span><span class="sxs-lookup"><span data-stu-id="c476f-224">In hello applications list, select **NetDocuments**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-netdocuments-tutorial/tutorial_netdocuments_app.png) 

3. <span data-ttu-id="c476f-226">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c476f-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c476f-228">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c476f-228">Click **Add** button.</span></span> <span data-ttu-id="c476f-229">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c476f-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c476f-231">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c476f-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c476f-232">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c476f-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c476f-233">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c476f-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c476f-234">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c476f-234">Testing single sign-on</span></span>

<span data-ttu-id="c476f-235">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c476f-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c476f-236">Quando você clica em Olá NetDocuments bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo NetDocuments.</span><span class="sxs-lookup"><span data-stu-id="c476f-236">When you click hello NetDocuments tile in hello Access Panel, you should get automatically signed-on tooyour NetDocuments application.</span></span>
<span data-ttu-id="c476f-237">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c476f-237">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c476f-238">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c476f-238">Additional resources</span></span>

* [<span data-ttu-id="c476f-239">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c476f-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c476f-240">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c476f-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-netdocuments-tutorial/tutorial_general_203.png

