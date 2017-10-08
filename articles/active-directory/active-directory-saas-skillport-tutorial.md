---
title: "Tutorial: integração do Azure Active Directory com o Skillport | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Skillport."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4df349b2-a73f-4b88-a077-ec0fbfc26527
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: ba504c3cae5f92767eb90d8453887904690fe0c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-skillport"></a><span data-ttu-id="4098c-103">Tutorial: integração do Azure Active Directory com o Skillport</span><span class="sxs-lookup"><span data-stu-id="4098c-103">Tutorial: Azure Active Directory integration with Skillport</span></span>

<span data-ttu-id="4098c-104">Neste tutorial, você aprenderá como toointegrate Skillport com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="4098c-104">In this tutorial, you learn how toointegrate Skillport with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4098c-105">Integrando Skillport com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="4098c-105">Integrating Skillport with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4098c-106">Você pode controlar no AD do Azure que tenha acesso tooSkillport</span><span class="sxs-lookup"><span data-stu-id="4098c-106">You can control in Azure AD who has access tooSkillport</span></span>
- <span data-ttu-id="4098c-107">Você pode habilitar seu usuários tooautomatically get conectado tooSkillport (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4098c-107">You can enable your users tooautomatically get signed-on tooSkillport (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4098c-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4098c-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4098c-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4098c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4098c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4098c-110">Prerequisites</span></span>

<span data-ttu-id="4098c-111">tooconfigure integração do AD do Azure com Skillport, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="4098c-111">tooconfigure Azure AD integration with Skillport, you need hello following items:</span></span>

- <span data-ttu-id="4098c-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4098c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4098c-113">Uma assinatura do Skillport com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="4098c-113">A Skillport single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4098c-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="4098c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4098c-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="4098c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4098c-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="4098c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4098c-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4098c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4098c-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="4098c-118">Scenario description</span></span>
<span data-ttu-id="4098c-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="4098c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4098c-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="4098c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4098c-121">Adicionando Skillport da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4098c-121">Adding Skillport from hello gallery</span></span>
2. <span data-ttu-id="4098c-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4098c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-skillport-from-hello-gallery"></a><span data-ttu-id="4098c-123">Adicionando Skillport da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="4098c-123">Adding Skillport from hello gallery</span></span>
<span data-ttu-id="4098c-124">integração de saudação tooconfigure de Skillport no AD do Azure, você precisa tooadd Skillport da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4098c-124">tooconfigure hello integration of Skillport into Azure AD, you need tooadd Skillport from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4098c-125">**tooadd Skillport da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4098c-125">**tooadd Skillport from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4098c-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4098c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4098c-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="4098c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4098c-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4098c-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="4098c-131">Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="4098c-131">Click **New Application** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="4098c-133">Na caixa de pesquisa hello, digite **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="4098c-133">In hello search box, type **Skillport**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_search.png)

5. <span data-ttu-id="4098c-135">No painel de resultados de saudação, selecione **Skillport**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4098c-135">In hello results panel, select **Skillport**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4098c-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4098c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4098c-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o Skillport com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="4098c-138">In this section, you configure and test Azure AD single sign-on with Skillport based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4098c-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Skillport é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="4098c-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Skillport is tooa user in Azure AD.</span></span> <span data-ttu-id="4098c-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Skillport precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="4098c-140">In other words, a link relationship between an Azure AD user and hello related user in Skillport needs toobe established.</span></span>

<span data-ttu-id="4098c-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Skillport.</span><span class="sxs-lookup"><span data-stu-id="4098c-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Skillport.</span></span>

<span data-ttu-id="4098c-142">tooconfigure e teste de logon único do AD do Azure com Skillport, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="4098c-142">tooconfigure and test Azure AD single sign-on with Skillport, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4098c-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="4098c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4098c-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4098c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4098c-145">**[Criar um usuário de teste Skillport](#creating-a-skillport-test-user)**  -toohave um equivalente do Britta Simon em Skillport é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="4098c-145">**[Creating a Skillport test user](#creating-a-skillport-test-user)** - toohave a counterpart of Britta Simon in Skillport that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4098c-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="4098c-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4098c-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="4098c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4098c-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="4098c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4098c-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Skillport.</span><span class="sxs-lookup"><span data-stu-id="4098c-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Skillport application.</span></span>

<span data-ttu-id="4098c-150">**tooconfigure AD do Azure-logon único com Skillport, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4098c-150">**tooconfigure Azure AD single sign-on with Skillport, perform hello following steps:**</span></span>

1. <span data-ttu-id="4098c-151">Em Olá portal do Azure, Olá **Skillport** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="4098c-151">In hello Azure  portal, on hello **Skillport** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="4098c-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="4098c-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_samlbase.png)

3. <span data-ttu-id="4098c-155">Em Olá **Skillport domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4098c-155">On hello **Skillport Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_url.png)

    <span data-ttu-id="4098c-157">a.</span><span class="sxs-lookup"><span data-stu-id="4098c-157">a.</span></span> <span data-ttu-id="4098c-158">Em Olá **URL de logon** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="4098c-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span>
      
      <span data-ttu-id="4098c-159">Datacenter da UE: `https://<subdomain>.skillport.eu`</span><span class="sxs-lookup"><span data-stu-id="4098c-159">EU Datacenter: `https://<subdomain>.skillport.eu`</span></span>
   
      <span data-ttu-id="4098c-160">Datacenter dos EUA: `https://<subdomain>.skillport.com`</span><span class="sxs-lookup"><span data-stu-id="4098c-160">US Datacenter: `https://<subdomain>.skillport.com`</span></span>
   
    <span data-ttu-id="4098c-161">b.</span><span class="sxs-lookup"><span data-stu-id="4098c-161">b.</span></span> <span data-ttu-id="4098c-162">Em Olá **URL de resposta** caixa de texto, digite uma URL usando Olá seguintes padrões:</span><span class="sxs-lookup"><span data-stu-id="4098c-162">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span>
    
      <span data-ttu-id="4098c-163">Datacenter da UE: `https://<subdomain>.skillport.eu/adfs/ls/`</span><span class="sxs-lookup"><span data-stu-id="4098c-163">EU Datacenter: `https://<subdomain>.skillport.eu/adfs/ls/`</span></span>
    
      <span data-ttu-id="4098c-164">Datacenter dos EUA: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span><span class="sxs-lookup"><span data-stu-id="4098c-164">US Datacenter: `https://<subdomain>.skillport.com/sp/ACS.saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4098c-165">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="4098c-165">These values are not hello real.</span></span> <span data-ttu-id="4098c-166">Atualize esses valores com URL de resposta real hello e a URL de logon.</span><span class="sxs-lookup"><span data-stu-id="4098c-166">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="4098c-167">Entre em contato com [equipe de suporte do cliente Skillport](https://www.skillsoft.com/contact.asp) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="4098c-167">Contact [Skillport Client support team](https://www.skillsoft.com/contact.asp) tooget these values.</span></span>
 
4. <span data-ttu-id="4098c-168">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="4098c-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_certificate.png) 

5. <span data-ttu-id="4098c-170">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="4098c-170">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-skillport-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4098c-172">tooconfigure logon único no **Skillport** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte Skillport](https://www.skillsoft.com/contact.asp).</span><span class="sxs-lookup"><span data-stu-id="4098c-172">tooconfigure single sign-on on **Skillport** side, you need toosend hello downloaded **Metadata XML** too[Skillport support team](https://www.skillsoft.com/contact.asp).</span></span> <span data-ttu-id="4098c-173">Eles serão configurá-lo toohave Olá conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="4098c-173">They will set it up toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4098c-174">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4098c-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="4098c-175">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4098c-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="4098c-177">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4098c-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4098c-178">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="4098c-178">In hello **Azure  portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skillport-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4098c-180">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="4098c-180">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skillport-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4098c-182">Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4098c-182">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skillport-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4098c-184">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4098c-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-skillport-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4098c-186">a.</span><span class="sxs-lookup"><span data-stu-id="4098c-186">a.</span></span> <span data-ttu-id="4098c-187">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4098c-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4098c-188">b.</span><span class="sxs-lookup"><span data-stu-id="4098c-188">b.</span></span> <span data-ttu-id="4098c-189">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4098c-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4098c-190">c.</span><span class="sxs-lookup"><span data-stu-id="4098c-190">c.</span></span> <span data-ttu-id="4098c-191">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="4098c-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4098c-192">d.</span><span class="sxs-lookup"><span data-stu-id="4098c-192">d.</span></span> <span data-ttu-id="4098c-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="4098c-193">Click **Create**.</span></span>
 
### <a name="creating-a-skillport-test-user"></a><span data-ttu-id="4098c-194">Criar um usuário de teste do Skillport</span><span class="sxs-lookup"><span data-stu-id="4098c-194">Creating a Skillport test user</span></span>

<span data-ttu-id="4098c-195">Usuário de teste do pedido toocreate Skillport, é necessário toocontact [Skillport a equipe de suporte](https://www.skillsoft.com/contact.asp) que eles têm vários cenários de negócios de acordo com o requisito de toohello de usuário final.</span><span class="sxs-lookup"><span data-stu-id="4098c-195">In order toocreate Skillport test user, you need toocontact [Skillport support team](https://www.skillsoft.com/contact.asp) as they have multiple business scenarios according toohello requirement of end user.</span></span> <span data-ttu-id="4098c-196">Ela configurará após discussão com usuários hello.</span><span class="sxs-lookup"><span data-stu-id="4098c-196">They will configure it after discussion with hello users.</span></span>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4098c-197">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="4098c-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4098c-198">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSkillport.</span><span class="sxs-lookup"><span data-stu-id="4098c-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSkillport.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="4098c-200">**tooassign Britta Simon tooSkillport, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="4098c-200">**tooassign Britta Simon tooSkillport, perform hello following steps:**</span></span>

1. <span data-ttu-id="4098c-201">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="4098c-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="4098c-203">Na lista de aplicativos hello, selecione **Skillport**.</span><span class="sxs-lookup"><span data-stu-id="4098c-203">In hello applications list, select **Skillport**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-skillport-tutorial/tutorial_skillport_app.png) 

3. <span data-ttu-id="4098c-205">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="4098c-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="4098c-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="4098c-207">Click **Add** button.</span></span> <span data-ttu-id="4098c-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4098c-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="4098c-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="4098c-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4098c-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4098c-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4098c-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="4098c-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4098c-213">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="4098c-213">Testing single sign-on</span></span>

<span data-ttu-id="4098c-214">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="4098c-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4098c-215">Quando você clica em bloco Skillport Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Skillport aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4098c-215">When you click hello Skillport tile in hello Access Panel, you should get automatically signed-on tooyour Skillport application.</span></span>
<span data-ttu-id="4098c-216">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="4098c-216">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="4098c-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="4098c-217">Additional resources</span></span>

* [<span data-ttu-id="4098c-218">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="4098c-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4098c-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4098c-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-skillport-tutorial/tutorial_general_203.png

