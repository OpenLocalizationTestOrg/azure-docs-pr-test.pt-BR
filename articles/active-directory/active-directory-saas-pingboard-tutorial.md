---
title: "Tutorial: Integração do Azure Active Directory com o Pingboard | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Pingboard."
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
ms.date: 04/04/2017
ms.author: jeedes
ms.openlocfilehash: 0a916b1f9ef32d8124aa11284d2115bb4fc0bbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-pingboard"></a><span data-ttu-id="cf248-103">Tutorial: Integração do Azure Active Directory ao Pingboard</span><span class="sxs-lookup"><span data-stu-id="cf248-103">Tutorial: Azure Active Directory integration with Pingboard</span></span>

<span data-ttu-id="cf248-104">Neste tutorial, você aprenderá como toointegrate Pingboard com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="cf248-104">In this tutorial, you learn how toointegrate Pingboard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cf248-105">Integrando Pingboard com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf248-105">Integrating Pingboard with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="cf248-106">Você pode controlar no AD do Azure que tenha acesso tooPingboard</span><span class="sxs-lookup"><span data-stu-id="cf248-106">You can control in Azure AD who has access tooPingboard</span></span>
- <span data-ttu-id="cf248-107">Você pode habilitar seu usuários tooautomatically get conectado tooPingboard (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cf248-107">You can enable your users tooautomatically get signed-on tooPingboard (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cf248-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="cf248-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="cf248-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cf248-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf248-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cf248-110">Prerequisites</span></span>

<span data-ttu-id="cf248-111">tooconfigure integração do AD do Azure com Pingboard, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf248-111">tooconfigure Azure AD integration with Pingboard, you need hello following items:</span></span>

- <span data-ttu-id="cf248-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cf248-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cf248-113">Uma assinatura do Pingboard habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="cf248-113">A Pingboard single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cf248-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="cf248-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cf248-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="cf248-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cf248-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="cf248-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="cf248-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cf248-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cf248-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="cf248-118">Scenario description</span></span>
<span data-ttu-id="cf248-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="cf248-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cf248-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="cf248-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cf248-121">Adicionando Pingboard da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="cf248-121">Adding Pingboard from hello gallery</span></span>
2. <span data-ttu-id="cf248-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cf248-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-pingboard-from-hello-gallery"></a><span data-ttu-id="cf248-123">Adicionando Pingboard da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="cf248-123">Adding Pingboard from hello gallery</span></span>
<span data-ttu-id="cf248-124">integração de saudação tooconfigure de Pingboard no AD do Azure, você precisa tooadd Pingboard da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="cf248-124">tooconfigure hello integration of Pingboard into Azure AD, you need tooadd Pingboard from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="cf248-125">**tooadd Pingboard da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cf248-125">**tooadd Pingboard from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf248-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="cf248-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cf248-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="cf248-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="cf248-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cf248-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="cf248-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf248-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="cf248-133">Na caixa de pesquisa hello, digite **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="cf248-133">In hello search box, type **Pingboard**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_search.png)

5. <span data-ttu-id="cf248-135">No painel de resultados de saudação, selecione **Pingboard**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="cf248-135">In hello results panel, select **Pingboard**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cf248-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cf248-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cf248-138">Nesta seção, você configura e testa o logon único do Azure AD com o Pingboard, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="cf248-138">In this section, you configure and test Azure AD single sign-on with Pingboard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cf248-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Pingboard é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf248-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Pingboard is tooa user in Azure AD.</span></span> <span data-ttu-id="cf248-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Pingboard precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="cf248-140">In other words, a link relationship between an Azure AD user and hello related user in Pingboard needs toobe established.</span></span>

<span data-ttu-id="cf248-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Pingboard.</span><span class="sxs-lookup"><span data-stu-id="cf248-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Pingboard.</span></span>

<span data-ttu-id="cf248-142">tooconfigure e teste de logon único do AD do Azure com Pingboard, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf248-142">tooconfigure and test Azure AD single sign-on with Pingboard, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="cf248-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="cf248-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="cf248-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf248-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cf248-145">**[Criar um usuário de teste Pingboard](#creating-a-pingboard-test-user)**  -toohave um equivalente do Britta Simon em Pingboard é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="cf248-145">**[Creating a Pingboard test user](#creating-a-pingboard-test-user)** - toohave a counterpart of Britta Simon in Pingboard that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="cf248-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="cf248-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cf248-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="cf248-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cf248-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf248-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cf248-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único no aplicativo Pingboard.</span><span class="sxs-lookup"><span data-stu-id="cf248-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Pingboard application.</span></span>

<span data-ttu-id="cf248-150">**tooconfigure AD do Azure-logon único com Pingboard, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cf248-150">**tooconfigure Azure AD single sign-on with Pingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf248-151">No portal de gerenciamento do Azure do hello, no hello **Pingboard** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="cf248-151">In hello Azure Management portal, on hello **Pingboard** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="cf248-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="cf248-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_samlbase.png)

3. <span data-ttu-id="cf248-155">Em Olá **Pingboard domínio e URLs** , execute Olá etapas a seguir se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="cf248-155">On hello **Pingboard Domain and URLs** section, perform hello following steps if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_url.png)

    <span data-ttu-id="cf248-157">a.</span><span class="sxs-lookup"><span data-stu-id="cf248-157">a.</span></span> <span data-ttu-id="cf248-158">Em Olá **identificador** texto, o valor do tipo hello como:`http://<entity-id>.pingboard.com/sp`</span><span class="sxs-lookup"><span data-stu-id="cf248-158">In hello **Identifier** textbox, type hello value as: `http://<entity-id>.pingboard.com/sp`</span></span>

    <span data-ttu-id="cf248-159">b.</span><span class="sxs-lookup"><span data-stu-id="cf248-159">b.</span></span> <span data-ttu-id="cf248-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<entity-id>.pingboard.com/auth/saml/consume`</span><span class="sxs-lookup"><span data-stu-id="cf248-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<entity-id>.pingboard.com/auth/saml/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cf248-161">Observe que esses não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf248-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="cf248-162">Você tem tooupdate esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf248-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="cf248-163">Aqui, é recomendável você toouse Olá valor exclusivo de cadeia de caracteres em identificador de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf248-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="cf248-164">Entre em contato com [equipe de suporte do cliente Pingboard](https://support.pingboard.com/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="cf248-164">Contact [Pingboard Client support team](https://support.pingboard.com/) tooget these values.</span></span> 

4. <span data-ttu-id="cf248-165">Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="cf248-165">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_sp_initiated01.png)

    <span data-ttu-id="cf248-167">a.</span><span class="sxs-lookup"><span data-stu-id="cf248-167">a.</span></span> <span data-ttu-id="cf248-168">Em Olá **URL de logon** texto, o valor do tipo hello como:`http://<sub-domain>.pingboard.com/sign_in`</span><span class="sxs-lookup"><span data-stu-id="cf248-168">In hello **Sign-on URL** textbox, type hello value as: `http://<sub-domain>.pingboard.com/sign_in`</span></span>
     
5. <span data-ttu-id="cf248-169">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="cf248-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_certificate.png) 

6. <span data-ttu-id="cf248-171">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="cf248-171">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="cf248-173">tooconfigure SSO no lado do Pingboard, abra uma nova janela do navegador e faça logon tooyour Pingboard conta.</span><span class="sxs-lookup"><span data-stu-id="cf248-173">tooconfigure SSO on Pingboard side, open a new browser window and log in tooyour Pingboard Account.</span></span> <span data-ttu-id="cf248-174">Você deve ser um tooset de admin Pingboard o logon único no.</span><span class="sxs-lookup"><span data-stu-id="cf248-174">You must be a Pingboard admin tooset up single sign on.</span></span>

8. <span data-ttu-id="cf248-175">No menu superior Olá selecione **aplicativos > integrações**</span><span class="sxs-lookup"><span data-stu-id="cf248-175">From hello top menu select **Apps > Integrations**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/Pingboard_integration.png)

9.  <span data-ttu-id="cf248-177">Em Olá **integrações** página, localize Olá **"Active Directory do Azure"** lado a lado e clique nele.</span><span class="sxs-lookup"><span data-stu-id="cf248-177">On hello **Integrations** page, find hello **"Azure Active Directory"** tile, and click it.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/Pingboard_aad.png)

10. <span data-ttu-id="cf248-179">Em Olá modal que segue clique **"Configurar"**</span><span class="sxs-lookup"><span data-stu-id="cf248-179">In hello modal that follows click **"Configure"**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/Pingboard_configure.png)

11. <span data-ttu-id="cf248-181">Em Olá página a seguir, você observará que "integração do Azure de SSO está habilitada.".</span><span class="sxs-lookup"><span data-stu-id="cf248-181">On hello following page, you will notice that "Azure SSO Integration is enabled.".</span></span> <span data-ttu-id="cf248-182">Abra Olá baixou o arquivo de Metadata XML em uma saudação de bloco de notas e cole o conteúdo no **metadados IDP**.</span><span class="sxs-lookup"><span data-stu-id="cf248-182">Open hello downloaded Metadata XML file in a notepad and paste hello content in **IDP Metadata**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/Pingboard_sso_configure.png)

12. <span data-ttu-id="cf248-184">arquivo Hello será validado e, se tudo estiver correto, o logon único será habilitado</span><span class="sxs-lookup"><span data-stu-id="cf248-184">hello file will be validated, and if everything is correct, single sign on will now be enabled</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cf248-185">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cf248-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="cf248-186">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf248-186">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="cf248-188">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cf248-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf248-189">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="cf248-189">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cf248-191">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="cf248-191">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cf248-193">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cf248-193">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cf248-195">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="cf248-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-pingboard-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cf248-197">a.</span><span class="sxs-lookup"><span data-stu-id="cf248-197">a.</span></span> <span data-ttu-id="cf248-198">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cf248-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cf248-199">b.</span><span class="sxs-lookup"><span data-stu-id="cf248-199">b.</span></span> <span data-ttu-id="cf248-200">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cf248-200">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cf248-201">c.</span><span class="sxs-lookup"><span data-stu-id="cf248-201">c.</span></span> <span data-ttu-id="cf248-202">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="cf248-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="cf248-203">d.</span><span class="sxs-lookup"><span data-stu-id="cf248-203">d.</span></span> <span data-ttu-id="cf248-204">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="cf248-204">Click **Create**.</span></span>
 
### <a name="creating-a-pingboard-test-user"></a><span data-ttu-id="cf248-205">Criando um usuário de teste do Pingboard</span><span class="sxs-lookup"><span data-stu-id="cf248-205">Creating a Pingboard test user</span></span>

<span data-ttu-id="cf248-206">Em ordem tooenable AD do Azure usuários toolog em Pingboard, eles devem ser provisionados no Pingboard.</span><span class="sxs-lookup"><span data-stu-id="cf248-206">In order tooenable Azure AD users toolog into Pingboard, they must be provisioned into Pingboard.</span></span>  
<span data-ttu-id="cf248-207">No caso de saudação de Pingboard, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="cf248-207">In hello case of Pingboard, provisioning is a manual task.</span></span>

<span data-ttu-id="cf248-208">**tooprovision contas de usuário, executar Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="cf248-208">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf248-209">Faça logon no tooyour Pingboard site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="cf248-209">Log in tooyour Pingboard company site as an administrator.</span></span>

2. <span data-ttu-id="cf248-210">Clique no botão **"Adicionar Funcionário"** na página **Diretório**.</span><span class="sxs-lookup"><span data-stu-id="cf248-210">Click **“Add Employee”** button on **Directory** page.</span></span>

    ![Adicionar Funcionário](./media/active-directory-saas-pingboard-tutorial/create_testuser_add.png)

3. <span data-ttu-id="cf248-212">Em Olá **"Adicionar funcionários"** caixa de diálogo de página, execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="cf248-212">On hello **“Add Employee”** dialog page, perform hello following steps.</span></span>

    ![Convidar Pessoas](./media/active-directory-saas-pingboard-tutorial/create_testuser_name.png)

    <span data-ttu-id="cf248-214">a.</span><span class="sxs-lookup"><span data-stu-id="cf248-214">a.</span></span> <span data-ttu-id="cf248-215">Em Olá **nome completo** caixa de texto, nome completo do tipo saudação do Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf248-215">In hello **Full Name** textbox, type hello full name of Britta Simon.</span></span>

    <span data-ttu-id="cf248-216">b.</span><span class="sxs-lookup"><span data-stu-id="cf248-216">b.</span></span> <span data-ttu-id="cf248-217">Em Olá **Email** caixa de texto, tipo hello endereço de email da conta de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf248-217">In hello **Email** textbox, type hello email address of Britta Simon account.</span></span>

    <span data-ttu-id="cf248-218">c.</span><span class="sxs-lookup"><span data-stu-id="cf248-218">c.</span></span> <span data-ttu-id="cf248-219">Em Olá **cargo** caixa de texto, tipo hello cargo do Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf248-219">In hello **Job Title** textbox, type hello job title of Britta Simon.</span></span>

    <span data-ttu-id="cf248-220">d.</span><span class="sxs-lookup"><span data-stu-id="cf248-220">d.</span></span> <span data-ttu-id="cf248-221">Em Olá **local** suspenso, local selecione saudação do Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf248-221">In hello **Location** dropdown, select hello location  of Britta Simon.</span></span>
    
    <span data-ttu-id="cf248-222">e.</span><span class="sxs-lookup"><span data-stu-id="cf248-222">e.</span></span> <span data-ttu-id="cf248-223">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cf248-223">Click **Add**.</span></span>   

4. <span data-ttu-id="cf248-224">Uma tela de confirmação aparecerá tooconfirm adição de saudação do usuário.</span><span class="sxs-lookup"><span data-stu-id="cf248-224">A confirmation screen will come up tooconfirm hello addition of user.</span></span>
    
    ![confirmar](./media/active-directory-saas-pingboard-tutorial/create_testuser_confirm.png)
        
    > [!NOTE]
    > <span data-ttu-id="cf248-226">proprietário de conta do Active Directory do Azure Olá será receberá um email e execute tooconfirm um link em sua conta antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="cf248-226">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="cf248-227">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="cf248-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="cf248-228">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooPingboard seu acesso.</span><span class="sxs-lookup"><span data-stu-id="cf248-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooPingboard.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="cf248-230">**tooassign Britta Simon tooPingboard, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="cf248-230">**tooassign Britta Simon tooPingboard, perform hello following steps:**</span></span>

1. <span data-ttu-id="cf248-231">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="cf248-231">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="cf248-233">Na lista de aplicativos hello, selecione **Pingboard**.</span><span class="sxs-lookup"><span data-stu-id="cf248-233">In hello applications list, select **Pingboard**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-pingboard-tutorial/tutorial_pingboard_app.png) 

3. <span data-ttu-id="cf248-235">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="cf248-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="cf248-237">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="cf248-237">Click **Add** button.</span></span> <span data-ttu-id="cf248-238">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cf248-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="cf248-240">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf248-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="cf248-241">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cf248-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cf248-242">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="cf248-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cf248-243">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="cf248-243">Testing single sign-on</span></span>

<span data-ttu-id="cf248-244">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="cf248-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="cf248-245">Quando você clica em bloco Pingboard Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Pingboard aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf248-245">When you click hello Pingboard tile in hello Access Panel, you should get automatically signed-on tooyour Pingboard application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cf248-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="cf248-246">Additional resources</span></span>

* [<span data-ttu-id="cf248-247">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="cf248-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cf248-248">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cf248-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-pingboard-tutorial/tutorial_general_203.png
