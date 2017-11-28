---
title: "Tutorial: Integração do Azure Active Directory com o Teamwork | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o trabalho em equipe."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03760032-3d76-4b47-ab84-241f72fbd561
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: jeedes
ms.openlocfilehash: f3a88a146f2a0a70de5ef58abd46f7f26b4104f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamwork"></a><span data-ttu-id="d80a3-103">Tutorial: Integração do Azure Active Directory ao Teamwork</span><span class="sxs-lookup"><span data-stu-id="d80a3-103">Tutorial: Azure Active Directory integration with Teamwork</span></span>

<span data-ttu-id="d80a3-104">Neste tutorial, você aprenderá como toointegrate equipe com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="d80a3-104">In this tutorial, you learn how toointegrate Teamwork with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d80a3-105">Integrar o trabalho em equipe com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="d80a3-105">Integrating Teamwork with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d80a3-106">Você pode controlar no AD do Azure que tenha acesso tooTeamwork</span><span class="sxs-lookup"><span data-stu-id="d80a3-106">You can control in Azure AD who has access tooTeamwork</span></span>
- <span data-ttu-id="d80a3-107">Você pode habilitar seu usuários tooautomatically get conectado tooTeamwork (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d80a3-107">You can enable your users tooautomatically get signed-on tooTeamwork (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d80a3-108">Você pode gerenciar suas contas em um local central – portal de gerenciamento do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="d80a3-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="d80a3-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d80a3-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d80a3-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d80a3-110">Prerequisites</span></span>

<span data-ttu-id="d80a3-111">tooconfigure integração do AD do Azure com o trabalho em equipe, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="d80a3-111">tooconfigure Azure AD integration with Teamwork, you need hello following items:</span></span>

- <span data-ttu-id="d80a3-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d80a3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d80a3-113">Uma assinatura do Teamwork habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="d80a3-113">A Teamwork single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="d80a3-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d80a3-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="d80a3-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d80a3-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d80a3-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d80a3-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d80a3-117">Se não tiver um ambiente de avaliação do Azure AD, você poderá obter uma avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d80a3-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="d80a3-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d80a3-118">Scenario description</span></span>
<span data-ttu-id="d80a3-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d80a3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d80a3-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="d80a3-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d80a3-121">Adicionando a equipe da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d80a3-121">Adding Teamwork from hello gallery</span></span>
2. <span data-ttu-id="d80a3-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d80a3-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-teamwork-from-hello-gallery"></a><span data-ttu-id="d80a3-123">Adicionando a equipe da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d80a3-123">Adding Teamwork from hello gallery</span></span>
<span data-ttu-id="d80a3-124">integração de saudação tooconfigure de colaboração em equipe no AD do Azure, você precisa tooadd equipe da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d80a3-124">tooconfigure hello integration of Teamwork into Azure AD, you need tooadd Teamwork from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d80a3-125">**tooadd equipe da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d80a3-125">**tooadd Teamwork from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d80a3-126">Em Olá  **[Portal de gerenciamento](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d80a3-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d80a3-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d80a3-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="d80a3-131">Clique em **adicionar** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d80a3-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="d80a3-133">Na caixa de pesquisa hello, digite **equipe**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-133">In hello search box, type **Teamwork**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_001.png)

5. <span data-ttu-id="d80a3-135">No painel de resultados de saudação, selecione **equipe**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d80a3-135">In hello results panel, select **Teamwork**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d80a3-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d80a3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d80a3-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Teamwork, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="d80a3-138">In this section, you configure and test Azure AD single sign-on with Teamwork based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d80a3-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na equipe é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d80a3-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamwork is tooa user in Azure AD.</span></span> <span data-ttu-id="d80a3-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na equipe precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="d80a3-140">In other words, a link relationship between an Azure AD user and hello related user in Teamwork needs toobe established.</span></span>

<span data-ttu-id="d80a3-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** na equipe.</span><span class="sxs-lookup"><span data-stu-id="d80a3-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamwork.</span></span>

<span data-ttu-id="d80a3-142">tooconfigure e teste de logon único do AD do Azure com o trabalho em equipe, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="d80a3-142">tooconfigure and test Azure AD single sign-on with Teamwork, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d80a3-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d80a3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d80a3-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d80a3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d80a3-145">**[Criar um usuário de teste da equipe](#creating-a-teamwork-test-user)**  -toohave um equivalente do Britta Simon em equipe é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="d80a3-145">**[Creating a Teamwork test user](#creating-a-teamwork-test-user)** - toohave a counterpart of Britta Simon in Teamwork that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="d80a3-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="d80a3-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d80a3-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="d80a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d80a3-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d80a3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d80a3-149">Nesta seção, habilitar o AD do Azure-logon único no portal de gerenciamento do Azure hello e configurar o logon único em seu aplicativo de equipe.</span><span class="sxs-lookup"><span data-stu-id="d80a3-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamwork application.</span></span>

<span data-ttu-id="d80a3-150">**tooconfigure AD do Azure-logon único com o trabalho em equipe, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d80a3-150">**tooconfigure Azure AD single sign-on with Teamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="d80a3-151">No portal de gerenciamento do Azure do hello, no hello **equipe** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-151">In hello Azure Management portal, on hello **Teamwork** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="d80a3-153">Em Olá **o logon único** caixa de diálogo, como **modo** selecione **baseado no SAML logon** tooenable de logon único.</span><span class="sxs-lookup"><span data-stu-id="d80a3-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_01.png)

3. <span data-ttu-id="d80a3-155">Em Olá **domínio de equipe e URLs** seção Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.teamwork.com`</span><span class="sxs-lookup"><span data-stu-id="d80a3-155">On hello **Teamwork Domain and URLs** section, in hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<company name>.teamwork.com`</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_02.png)

    > [!NOTE] 
    > <span data-ttu-id="d80a3-157">Observe que isso não é um valor real hello.</span><span class="sxs-lookup"><span data-stu-id="d80a3-157">Please note that this is not hello real value.</span></span> <span data-ttu-id="d80a3-158">Você tem tooupdate esse valor com hello real URL de logon.</span><span class="sxs-lookup"><span data-stu-id="d80a3-158">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="d80a3-159">Entre em contato com [equipe de suporte da equipe](mailto:support@teamwork.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="d80a3-159">Contact [Teamwork support team](mailto:support@teamwork.com) tooget this value.</span></span> 

4. <span data-ttu-id="d80a3-160">Em Olá **o certificado de autenticação SAML** seção, clique em **criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-160">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_03.png)   

5. <span data-ttu-id="d80a3-162">Em Olá **criar um novo certificado** caixa de diálogo, clique o ícone de calendário hello e selecione um **data de expiração**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-162">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="d80a3-163">Em seguida, clique no botão **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-163">Then click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamwork-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="d80a3-165">Em Olá **o certificado de autenticação SAML** seção, selecione **ativar o novo certificado** e clique em **salvar** botão.</span><span class="sxs-lookup"><span data-stu-id="d80a3-165">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_04.png)

7. <span data-ttu-id="d80a3-167">Na janela pop-up de saudação **certificado de substituição** janela, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-167">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamwork-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="d80a3-169">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d80a3-169">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_05.png) 

9. <span data-ttu-id="d80a3-171">tooget SSO configurado para o seu aplicativo, entre em contato com [equipe de suporte da equipe](mailto:support@teamwork.com) e fornecê-los com hello baixado **metadados**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-171">tooget SSO configured for your application, contact [Teamwork support team](mailto:support@teamwork.com) and provide them with hello downloaded **metadata**.</span></span>
  

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d80a3-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d80a3-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="d80a3-173">Olá o objetivo desta seção é toocreate um usuário de teste no portal de gerenciamento do Azure Olá chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d80a3-173">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="d80a3-175">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d80a3-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d80a3-176">Em Olá **portal de gerenciamento do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d80a3-176">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamwork-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d80a3-178">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="d80a3-178">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamwork-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d80a3-180">Na parte superior de saudação da caixa de diálogo Olá clique **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d80a3-180">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamwork-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d80a3-182">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d80a3-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-teamwork-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d80a3-184">a.</span><span class="sxs-lookup"><span data-stu-id="d80a3-184">a.</span></span> <span data-ttu-id="d80a3-185">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d80a3-186">b.</span><span class="sxs-lookup"><span data-stu-id="d80a3-186">b.</span></span> <span data-ttu-id="d80a3-187">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d80a3-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d80a3-188">c.</span><span class="sxs-lookup"><span data-stu-id="d80a3-188">c.</span></span> <span data-ttu-id="d80a3-189">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d80a3-190">d.</span><span class="sxs-lookup"><span data-stu-id="d80a3-190">d.</span></span> <span data-ttu-id="d80a3-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-191">Click **Create**.</span></span> 



### <a name="creating-a-teamwork-test-user"></a><span data-ttu-id="d80a3-192">Criar um usuário de teste do Teamwork</span><span class="sxs-lookup"><span data-stu-id="d80a3-192">Creating a Teamwork test user</span></span>

<span data-ttu-id="d80a3-193">Nesta seção, você criará uma usuária chamado Brenda Fernandes no Teamwork.</span><span class="sxs-lookup"><span data-stu-id="d80a3-193">In this section, you create a user called Britta Simon in Teamwork.</span></span> <span data-ttu-id="d80a3-194">Trabalhe com [equipe de suporte da equipe](mailto:support@teamwork.com) tooadd usuários de saudação na plataforma de equipe hello.</span><span class="sxs-lookup"><span data-stu-id="d80a3-194">Please work with [Teamwork support team](mailto:support@teamwork.com) tooadd hello users in hello Teamwork platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d80a3-195">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d80a3-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d80a3-196">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooTeamwork seu acesso.</span><span class="sxs-lookup"><span data-stu-id="d80a3-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamwork.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="d80a3-198">**tooassign Britta Simon tooTeamwork, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d80a3-198">**tooassign Britta Simon tooTeamwork, perform hello following steps:**</span></span>

1. <span data-ttu-id="d80a3-199">No portal de gerenciamento do Azure hello, abrir modo de exibição de aplicativos Olá e, em seguida, navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-199">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d80a3-201">Na lista de aplicativos hello, selecione **equipe**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-201">In hello applications list, select **Teamwork**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-teamwork-tutorial/tutorial_teamwork_50.png) 

3. <span data-ttu-id="d80a3-203">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="d80a3-205">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d80a3-205">Click **Add** button.</span></span> <span data-ttu-id="d80a3-206">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d80a3-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="d80a3-208">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="d80a3-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d80a3-209">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d80a3-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d80a3-210">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d80a3-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="d80a3-211">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="d80a3-211">Testing single sign-on</span></span>

<span data-ttu-id="d80a3-212">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d80a3-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d80a3-213">Quando você clica em um bloco de equipe Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de equipe.</span><span class="sxs-lookup"><span data-stu-id="d80a3-213">When you click hello Teamwork tile in hello Access Panel, you should get automatically signed-on tooyour Teamwork application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d80a3-214">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d80a3-214">Additional resources</span></span>

* [<span data-ttu-id="d80a3-215">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d80a3-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d80a3-216">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d80a3-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamwork-tutorial/tutorial_general_203.png