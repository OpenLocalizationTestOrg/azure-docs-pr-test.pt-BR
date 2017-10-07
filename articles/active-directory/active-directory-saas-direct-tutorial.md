---
title: "Tutorial: Integração do Azure Active Directory ao Direct | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e direto."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ac663070b39e55eade2c43814b63a9d0374c7316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="97601-103">Tutorial: integração do Azure Active Directory com o Direct</span><span class="sxs-lookup"><span data-stu-id="97601-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="97601-104">Neste tutorial, você aprenderá como toointegrate direta com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="97601-104">In this tutorial, you learn how toointegrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="97601-105">Integração direta com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="97601-105">Integrating Direct with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="97601-106">Você pode controlar no AD do Azure que tenha acesso tooDirect</span><span class="sxs-lookup"><span data-stu-id="97601-106">You can control in Azure AD who has access tooDirect</span></span>
- <span data-ttu-id="97601-107">Você pode habilitar seu usuários tooautomatically get conectado tooDirect (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="97601-107">You can enable your users tooautomatically get signed-on tooDirect (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="97601-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="97601-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="97601-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="97601-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97601-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="97601-110">Prerequisites</span></span>

<span data-ttu-id="97601-111">tooconfigure integração do AD do Azure com o Direct, é necessário Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="97601-111">tooconfigure Azure AD integration with Direct, you need hello following items:</span></span>

- <span data-ttu-id="97601-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="97601-112">An Azure AD subscription</span></span>
- <span data-ttu-id="97601-113">Uma assinatura habilitada para logon único do Direct</span><span class="sxs-lookup"><span data-stu-id="97601-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="97601-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="97601-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="97601-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="97601-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="97601-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="97601-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="97601-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97601-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="97601-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="97601-118">Scenario description</span></span>
<span data-ttu-id="97601-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="97601-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="97601-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="97601-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="97601-121">Adicionando diretamente da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="97601-121">Adding Direct from hello gallery</span></span>
2. <span data-ttu-id="97601-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="97601-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-hello-gallery"></a><span data-ttu-id="97601-123">Adicionando diretamente da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="97601-123">Adding Direct from hello gallery</span></span>
<span data-ttu-id="97601-124">integração de saudação tooconfigure do Direct no AD do Azure, você precisa tooadd direta da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="97601-124">tooconfigure hello integration of Direct into Azure AD, you need tooadd Direct from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="97601-125">**tooadd direta da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="97601-125">**tooadd Direct from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="97601-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="97601-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="97601-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="97601-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="97601-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="97601-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="97601-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="97601-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="97601-133">Na caixa de pesquisa hello, digite **direto**.</span><span class="sxs-lookup"><span data-stu-id="97601-133">In hello search box, type **Direct**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="97601-135">No painel de resultados de saudação, selecione **direto**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="97601-135">In hello results panel, select **Direct**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="97601-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="97601-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="97601-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Direct com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="97601-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="97601-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em direta é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="97601-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Direct is tooa user in Azure AD.</span></span> <span data-ttu-id="97601-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em toobe necessidades diretas estabelecida.</span><span class="sxs-lookup"><span data-stu-id="97601-140">In other words, a link relationship between an Azure AD user and hello related user in Direct needs toobe established.</span></span>

<span data-ttu-id="97601-141">Diretas, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="97601-141">In Direct, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="97601-142">teste do AD do Azure e tooconfigure o logon único com o Direct, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="97601-142">tooconfigure and test Azure AD single sign-on with Direct, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="97601-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="97601-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="97601-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="97601-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="97601-145">**[Criar um usuário de teste direto](#creating-a-direct-test-user)**  -toohave um equivalente do Britta Simon diretas que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="97601-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - toohave a counterpart of Britta Simon in Direct that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="97601-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="97601-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="97601-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="97601-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="97601-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="97601-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="97601-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo direto.</span><span class="sxs-lookup"><span data-stu-id="97601-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="97601-150">**tooconfigure logon único do AD do Azure com o Direct, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="97601-150">**tooconfigure Azure AD single sign-on with Direct, perform hello following steps:**</span></span>

1. <span data-ttu-id="97601-151">Em Olá portal do Azure, Olá **direto** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="97601-151">In hello Azure portal, on hello **Direct** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="97601-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="97601-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="97601-155">Em Olá **domínio direto e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="97601-155">On hello **Direct Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="97601-157">Em Olá **identificador** caixa de texto, digite a URL de saudação:`https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="97601-157">In hello **Identifier** textbox, type hello URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="97601-158">Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="97601-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="97601-160">Em Olá **URL de logon** caixa de texto, digite a URL de saudação:`https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="97601-160">In hello **Sign-on URL** textbox, type hello URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="97601-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="97601-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="97601-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="97601-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="97601-165">tooconfigure logon único no **direto** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte direto](https://direct4b.com/ja/support.html#inquiry).</span><span class="sxs-lookup"><span data-stu-id="97601-165">tooconfigure single sign-on on **Direct** side, you need toosend hello downloaded **Metadata XML** too[Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="97601-166">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="97601-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="97601-167">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="97601-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="97601-168">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="97601-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="97601-169">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="97601-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="97601-170">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="97601-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="97601-172">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="97601-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="97601-173">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="97601-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="97601-175">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="97601-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="97601-177">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="97601-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="97601-179">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="97601-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="97601-181">a.</span><span class="sxs-lookup"><span data-stu-id="97601-181">a.</span></span> <span data-ttu-id="97601-182">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="97601-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="97601-183">b.</span><span class="sxs-lookup"><span data-stu-id="97601-183">b.</span></span> <span data-ttu-id="97601-184">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="97601-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="97601-185">c.</span><span class="sxs-lookup"><span data-stu-id="97601-185">c.</span></span> <span data-ttu-id="97601-186">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="97601-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="97601-187">d.</span><span class="sxs-lookup"><span data-stu-id="97601-187">d.</span></span> <span data-ttu-id="97601-188">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="97601-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="97601-189">Como criar um usuário de teste do Direct</span><span class="sxs-lookup"><span data-stu-id="97601-189">Creating a Direct test user</span></span>

<span data-ttu-id="97601-190">Nesta seção, você criará um usuário chamado Brenda Fernandes no Direct.</span><span class="sxs-lookup"><span data-stu-id="97601-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="97601-191">Trabalhar com [a equipe de suporte direto](https://direct4b.com/ja/support.html#inquiry) para adicionar usuários de saudação na plataforma de saudação direto.</span><span class="sxs-lookup"><span data-stu-id="97601-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add hello users in hello Direct platform.</span></span> <span data-ttu-id="97601-192">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="97601-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="97601-193">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="97601-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="97601-194">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooDirect.</span><span class="sxs-lookup"><span data-stu-id="97601-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDirect.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="97601-196">**tooassign Britta Simon tooDirect, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="97601-196">**tooassign Britta Simon tooDirect, perform hello following steps:**</span></span>

1. <span data-ttu-id="97601-197">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="97601-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="97601-199">Na lista de aplicativos hello, selecione **direto**.</span><span class="sxs-lookup"><span data-stu-id="97601-199">In hello applications list, select **Direct**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="97601-201">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="97601-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="97601-203">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="97601-203">Click **Add** button.</span></span> <span data-ttu-id="97601-204">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="97601-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="97601-206">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="97601-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="97601-207">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="97601-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="97601-208">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="97601-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="97601-209">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="97601-209">Testing single sign-on</span></span>

<span data-ttu-id="97601-210">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="97601-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

1. <span data-ttu-id="97601-211">Se você quiser tootest em **IDP iniciada modo**:</span><span class="sxs-lookup"><span data-stu-id="97601-211">If you wish tootest in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="97601-212">Quando você clica em Olá **direto** Olá de bloco no painel de acesso, você deve obter automaticamente assinado em tooyour **direto** aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97601-212">When you click hello **Direct** tile in hello Access Panel, you should get automatically signed-on tooyour **Direct** application.</span></span>

2. <span data-ttu-id="97601-213">Se você quiser tootest em **modo iniciado do SP**:</span><span class="sxs-lookup"><span data-stu-id="97601-213">If you wish tootest in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="97601-214">a.</span><span class="sxs-lookup"><span data-stu-id="97601-214">a.</span></span> <span data-ttu-id="97601-215">Clique em Olá **direto** lado a lado no painel de acesso de saudação e você será redirecionado toohello aplicativo logon na página.</span><span class="sxs-lookup"><span data-stu-id="97601-215">Click on hello **Direct** tile in hello Access Panel and you will be redirected toohello application sign-on page.</span></span>

    <span data-ttu-id="97601-216">b.</span><span class="sxs-lookup"><span data-stu-id="97601-216">b.</span></span> <span data-ttu-id="97601-217">Entrada seu `subdomain` na caixa de texto de saudação exibida e pressione '次へ (Avançar)' e você deve obter automaticamente assinado em tooyour **direto** aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97601-217">Input your `subdomain` in hello textbox displayed and press '次へ (Next)' and you should get automatically signed-on tooyour **Direct** application .</span></span>
    
<span data-ttu-id="97601-218">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="97601-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="97601-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="97601-219">Additional resources</span></span>

* [<span data-ttu-id="97601-220">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="97601-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="97601-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="97601-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

