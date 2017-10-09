---
title: "Tutorial: integração do Azure Active Directory com o Land Gorilla Client | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Gorilla Terra."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: jeedes
ms.openlocfilehash: e95a30551e636108fe22a7ab6d1827bc12d7f9a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-land-gorilla-client"></a><span data-ttu-id="62a79-103">Tutorial: integração do Azure Active Directory com o Land Gorilla Client</span><span class="sxs-lookup"><span data-stu-id="62a79-103">Tutorial: Azure Active Directory integration with Land Gorilla Client</span></span>

<span data-ttu-id="62a79-104">Neste tutorial, você aprenderá como toointegrate Terra Gorilla cliente com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="62a79-104">In this tutorial, you learn how toointegrate Land Gorilla Client with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62a79-105">Integrando Terra Gorilla cliente com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="62a79-105">Integrating Land Gorilla Client with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="62a79-106">Você pode controlar no AD do Azure que tenha acesso tooLand Gorilla cliente</span><span class="sxs-lookup"><span data-stu-id="62a79-106">You can control in Azure AD who has access tooLand Gorilla Client</span></span>
- <span data-ttu-id="62a79-107">Você pode habilitar seu usuários tooautomatically get conectado tooLand cliente Gorilla (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62a79-107">You can enable your users tooautomatically get signed-on tooLand Gorilla Client (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62a79-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="62a79-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="62a79-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="62a79-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="62a79-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="62a79-110">Prerequisites</span></span>

<span data-ttu-id="62a79-111">tooconfigure integração do AD do Azure com Terra Gorilla cliente, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="62a79-111">tooconfigure Azure AD integration with Land Gorilla Client, you need hello following items:</span></span>

- <span data-ttu-id="62a79-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62a79-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62a79-113">Uma assinatura do Land Gorilla Client habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="62a79-113">A Land Gorilla Client single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="62a79-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="62a79-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="62a79-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="62a79-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62a79-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="62a79-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="62a79-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62a79-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="62a79-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="62a79-118">Scenario description</span></span>
<span data-ttu-id="62a79-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="62a79-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62a79-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="62a79-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62a79-121">Adicionar cliente ao Gorilla terra da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="62a79-121">Adding Land Gorilla Client from hello gallery</span></span>
2. <span data-ttu-id="62a79-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62a79-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-land-gorilla-client-from-hello-gallery"></a><span data-ttu-id="62a79-123">Adicionar cliente ao Gorilla terra da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="62a79-123">Adding Land Gorilla Client from hello gallery</span></span>
<span data-ttu-id="62a79-124">integração de Olá tooconfigure da Terra Gorilla cliente no AD do Azure, você precisa de terra tooadd Gorilla cliente da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="62a79-124">tooconfigure hello integration of Land Gorilla Client into Azure AD, you need tooadd Land Gorilla Client from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="62a79-125">**tooadd Terra Gorilla cliente da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="62a79-125">**tooadd Land Gorilla Client from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="62a79-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="62a79-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="62a79-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="62a79-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="62a79-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="62a79-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="62a79-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="62a79-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="62a79-133">Na caixa de pesquisa hello, digite **Terra Gorilla cliente**.</span><span class="sxs-lookup"><span data-stu-id="62a79-133">In hello search box, type **Land Gorilla Client**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_search.png)

5. <span data-ttu-id="62a79-135">No painel de resultados de saudação, selecione **Terra Gorilla cliente**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="62a79-135">In hello results panel, select **Land Gorilla Client**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62a79-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62a79-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62a79-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Land Gorilla Client, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="62a79-138">In this section, you configure and test Azure AD single sign-on with Land Gorilla Client based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62a79-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na Terra Gorilla cliente é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="62a79-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Land Gorilla Client is tooa user in Azure AD.</span></span> <span data-ttu-id="62a79-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na Terra Gorilla cliente precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="62a79-140">In other words, a link relationship between an Azure AD user and hello related user in Land Gorilla Client needs toobe established.</span></span>

<span data-ttu-id="62a79-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** na Terra Gorilla cliente.</span><span class="sxs-lookup"><span data-stu-id="62a79-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Land Gorilla Client.</span></span>

<span data-ttu-id="62a79-142">tooconfigure e teste de logon único do AD do Azure com Terra Gorilla cliente, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="62a79-142">tooconfigure and test Azure AD single sign-on with Land Gorilla Client, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="62a79-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="62a79-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="62a79-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com um grupo limitado.</span><span class="sxs-lookup"><span data-stu-id="62a79-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with limited group.</span></span>
3. <span data-ttu-id="62a79-145">**[Criar um usuário de teste de terra Gorilla](#creating-a-land-gorilla-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62a79-145">**[Creating a Land Gorilla test user](#creating-a-land-gorilla-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="62a79-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="62a79-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62a79-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="62a79-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62a79-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="62a79-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62a79-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo cliente de Gorilla Terra.</span><span class="sxs-lookup"><span data-stu-id="62a79-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Land Gorilla Client application.</span></span>

<span data-ttu-id="62a79-150">**tooconfigure logon único do AD do Azure com o cliente Gorilla Terra, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="62a79-150">**tooconfigure Azure AD single sign-on with Land Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="62a79-151">No portal de gerenciamento do Azure do hello, no hello **Terra Gorilla cliente** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="62a79-151">In hello Azure Management portal, on hello **Land Gorilla Client** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="62a79-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="62a79-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_samlbase.png)

3. <span data-ttu-id="62a79-155">Em Olá **URLs e domínio de cliente Gorilla Terra** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="62a79-155">On hello **Land Gorilla Client Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_url_02.png)

    <span data-ttu-id="62a79-157">a.</span><span class="sxs-lookup"><span data-stu-id="62a79-157">a.</span></span> <span data-ttu-id="62a79-158">Em Olá **identificador** texto, o valor do tipo hello usando uma saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="62a79-158">In hello **Identifier** textbox, type hello value using one of hello following pattern:</span></span> 
    
    `https://<customer domain>.landgorilla.com/` 
    
    `https://www.<customer domain>.landgorilla.com`

    <span data-ttu-id="62a79-159">b.</span><span class="sxs-lookup"><span data-stu-id="62a79-159">b.</span></span> <span data-ttu-id="62a79-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando uma saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="62a79-160">In hello **Reply URL** textbox, type a URL using one of hello following pattern:</span></span>

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/core/authenticate.php`

    `https://<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`
    
    `https://www.<customer domain>.landgorilla.com/simplesaml/module.php/saml/sp/saml2-acs.php/default-sp`

    > [!NOTE] 
    > <span data-ttu-id="62a79-161">Observe que esses não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="62a79-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="62a79-162">Você tem tooupdate esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="62a79-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="62a79-163">Aqui, é recomendável você toouse Olá valor exclusivo de cadeia de caracteres em identificador de saudação.</span><span class="sxs-lookup"><span data-stu-id="62a79-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="62a79-164">Entre em contato com [equipe Terra Gorilla cliente](https://www.landgorilla.com/support/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="62a79-164">Contact [Land Gorilla Client team](https://www.landgorilla.com/support/) tooget these values.</span></span> 

4. <span data-ttu-id="62a79-165">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="62a79-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_certificate.png) 

5. <span data-ttu-id="62a79-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="62a79-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-landgorilla-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="62a79-169">configuração de SSO de tooget concluída para o seu aplicativo final Gorilla Terra, entre em contato com [equipe de suporte de terra Gorilla cliente](https://www.landgorilla.com/support/) e fornecê-los com hello baixado **"Metadata XML** arquivo.</span><span class="sxs-lookup"><span data-stu-id="62a79-169">tooget SSO configuration complete for your application at Land Gorilla end, Contact [Land Gorilla Client support team](https://www.landgorilla.com/support/) and provide them with hello downloaded **“Metadata XML** file.</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62a79-170">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62a79-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="62a79-171">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62a79-171">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="62a79-173">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="62a79-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="62a79-174">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="62a79-174">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="62a79-176">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="62a79-176">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="62a79-178">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="62a79-178">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62a79-180">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="62a79-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-landgorilla-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="62a79-182">a.</span><span class="sxs-lookup"><span data-stu-id="62a79-182">a.</span></span> <span data-ttu-id="62a79-183">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62a79-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62a79-184">b.</span><span class="sxs-lookup"><span data-stu-id="62a79-184">b.</span></span> <span data-ttu-id="62a79-185">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="62a79-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="62a79-186">c.</span><span class="sxs-lookup"><span data-stu-id="62a79-186">c.</span></span> <span data-ttu-id="62a79-187">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="62a79-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="62a79-188">d.</span><span class="sxs-lookup"><span data-stu-id="62a79-188">d.</span></span> <span data-ttu-id="62a79-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="62a79-189">Click **Create**.</span></span> 

### <a name="creating-a-land-gorilla-test-user"></a><span data-ttu-id="62a79-190">Criar um usuário de teste do Land Gorilla</span><span class="sxs-lookup"><span data-stu-id="62a79-190">Creating a Land Gorilla test user</span></span>

<span data-ttu-id="62a79-191">Trabalhe com [equipe de suporte de terra Gorilla](https://www.landgorilla.com/support/) tooadd usuários de saudação na plataforma de terra Gorilla hello.</span><span class="sxs-lookup"><span data-stu-id="62a79-191">Please work with [Land Gorilla support team](https://www.landgorilla.com/support/) tooadd hello users in hello Land Gorilla platform.</span></span>
    
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="62a79-192">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="62a79-192">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="62a79-193">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooLand seu acesso cliente Gorilla.</span><span class="sxs-lookup"><span data-stu-id="62a79-193">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLand Gorilla Client.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="62a79-195">**tooassign Britta Simon tooLand Gorilla cliente, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="62a79-195">**tooassign Britta Simon tooLand Gorilla Client, perform hello following steps:**</span></span>

1. <span data-ttu-id="62a79-196">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="62a79-196">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="62a79-198">Na lista de aplicativos hello, selecione **Terra Gorilla cliente**.</span><span class="sxs-lookup"><span data-stu-id="62a79-198">In hello applications list, select **Land Gorilla Client**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-landgorilla-tutorial/tutorial_landgorilla_app.png) 

3. <span data-ttu-id="62a79-200">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="62a79-200">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="62a79-202">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="62a79-202">Click **Add** button.</span></span> <span data-ttu-id="62a79-203">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="62a79-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="62a79-205">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="62a79-205">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="62a79-206">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="62a79-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62a79-207">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="62a79-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="62a79-208">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="62a79-208">Testing single sign-on</span></span>

<span data-ttu-id="62a79-209">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="62a79-209">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="62a79-210">Quando você clica em um bloco de terra Gorilla cliente Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo cliente de Gorilla Terra.</span><span class="sxs-lookup"><span data-stu-id="62a79-210">When you click hello Land Gorilla Client tile in hello Access Panel, you should get automatically signed-on tooyour Land Gorilla Client application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="62a79-211">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="62a79-211">Additional resources</span></span>

* [<span data-ttu-id="62a79-212">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="62a79-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62a79-213">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="62a79-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-landgorilla-tutorial/tutorial_general_203.png
