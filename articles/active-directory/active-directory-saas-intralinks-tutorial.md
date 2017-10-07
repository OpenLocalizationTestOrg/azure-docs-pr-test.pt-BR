---
title: "Tutorial: integração do Azure Active Directory com o Intralinks | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Intralinks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 6fa49c932d0c48d4b48e04fe91af9fc86a0c1cdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="1ad5e-103">Tutorial: Integração do Azure Active Directory com o Intralinks</span><span class="sxs-lookup"><span data-stu-id="1ad5e-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="1ad5e-104">Neste tutorial, você aprenderá como toointegrate Intralinks com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="1ad5e-104">In this tutorial, you learn how toointegrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1ad5e-105">Integrando Intralinks com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ad5e-105">Integrating Intralinks with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1ad5e-106">Você pode controlar no AD do Azure que tenha acesso tooIntralinks</span><span class="sxs-lookup"><span data-stu-id="1ad5e-106">You can control in Azure AD who has access tooIntralinks</span></span>
- <span data-ttu-id="1ad5e-107">Você pode habilitar seus usuários tooautomatically get conectado tooIntralinks (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1ad5e-107">You can enable your users tooautomatically get signed-on tooIntralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1ad5e-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1ad5e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1ad5e-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1ad5e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ad5e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1ad5e-110">Prerequisites</span></span>

<span data-ttu-id="1ad5e-111">tooconfigure integração do AD do Azure com Intralinks, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ad5e-111">tooconfigure Azure AD integration with Intralinks, you need hello following items:</span></span>

- <span data-ttu-id="1ad5e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1ad5e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1ad5e-113">Uma assinatura habilitada para logon único do Intralinks</span><span class="sxs-lookup"><span data-stu-id="1ad5e-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1ad5e-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1ad5e-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1ad5e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1ad5e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1ad5e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1ad5e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1ad5e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1ad5e-118">Scenario description</span></span>
<span data-ttu-id="1ad5e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1ad5e-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="1ad5e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1ad5e-121">Adicionando Intralinks da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1ad5e-121">Adding Intralinks from hello gallery</span></span>
2. <span data-ttu-id="1ad5e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1ad5e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-hello-gallery"></a><span data-ttu-id="1ad5e-123">Adicionando Intralinks da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1ad5e-123">Adding Intralinks from hello gallery</span></span>
<span data-ttu-id="1ad5e-124">integração de saudação tooconfigure de Intralinks no AD do Azure, você precisa tooadd Intralinks da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-124">tooconfigure hello integration of Intralinks into Azure AD, you need tooadd Intralinks from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1ad5e-125">**tooadd Intralinks da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1ad5e-125">**tooadd Intralinks from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ad5e-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1ad5e-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1ad5e-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1ad5e-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1ad5e-133">Na caixa de pesquisa hello, digite **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-133">In hello search box, type **Intralinks**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="1ad5e-135">No painel de resultados de saudação, selecione **Intralinks**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-135">In hello results panel, select **Intralinks**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1ad5e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1ad5e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1ad5e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Intralinks, com base em uma usuária de teste chamada "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="1ad5e-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1ad5e-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Intralinks é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Intralinks is tooa user in Azure AD.</span></span> <span data-ttu-id="1ad5e-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Intralinks precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-140">In other words, a link relationship between an Azure AD user and hello related user in Intralinks needs toobe established.</span></span>

<span data-ttu-id="1ad5e-141">Intralinks, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-141">In Intralinks, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1ad5e-142">tooconfigure e teste de logon único do AD do Azure com Intralinks, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ad5e-142">tooconfigure and test Azure AD single sign-on with Intralinks, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1ad5e-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1ad5e-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1ad5e-145">**[Criar um usuário de teste Intralinks](#creating-an-intralinks-test-user)**  -toohave um equivalente do Britta Simon em Intralinks é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - toohave a counterpart of Britta Simon in Intralinks that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1ad5e-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1ad5e-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1ad5e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ad5e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1ad5e-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Intralinks.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="1ad5e-150">**tooconfigure AD do Azure-logon único com Intralinks, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1ad5e-150">**tooconfigure Azure AD single sign-on with Intralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ad5e-151">Em Olá portal do Azure, Olá **Intralinks** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-151">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1ad5e-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="1ad5e-155">Em Olá **Intralinks domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ad5e-155">On hello **Intralinks Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="1ad5e-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span><span class="sxs-lookup"><span data-stu-id="1ad5e-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1ad5e-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-158">This value is not real.</span></span> <span data-ttu-id="1ad5e-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="1ad5e-160">Entre em contato com [equipe de suporte do cliente Intralinks](https://www.intralinks.com/contact-1) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) tooget this value.</span></span> 
 
4. <span data-ttu-id="1ad5e-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="1ad5e-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1ad5e-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="1ad5e-165">tooconfigure logon único no **Intralinks** lado, você precisa toosend Olá baixado **Metadata XML** [equipe de suporte do Intralinks](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="1ad5e-165">tooconfigure single sign-on on **Intralinks** side, you need toosend hello downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="1ad5e-166">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="1ad5e-167">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="1ad5e-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1ad5e-168">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1ad5e-169">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1ad5e-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1ad5e-170">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1ad5e-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="1ad5e-171">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1ad5e-173">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1ad5e-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ad5e-174">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1ad5e-176">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1ad5e-178">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1ad5e-180">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ad5e-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1ad5e-182">a.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-182">a.</span></span> <span data-ttu-id="1ad5e-183">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1ad5e-184">b.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-184">b.</span></span> <span data-ttu-id="1ad5e-185">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1ad5e-186">c.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-186">c.</span></span> <span data-ttu-id="1ad5e-187">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1ad5e-188">d.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-188">d.</span></span> <span data-ttu-id="1ad5e-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="1ad5e-190">Criação de um usuário de teste do Intralinks</span><span class="sxs-lookup"><span data-stu-id="1ad5e-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="1ad5e-191">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Intralinks.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="1ad5e-192">Trabalhe com [Intralinks equipe de suporte](https://www.intralinks.com/contact-1) tooadd usuários de saudação na plataforma de Intralinks hello.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) tooadd hello users in hello Intralinks platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1ad5e-193">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1ad5e-193">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1ad5e-194">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooIntralinks.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIntralinks.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1ad5e-196">**tooassign Britta Simon tooIntralinks, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1ad5e-196">**tooassign Britta Simon tooIntralinks, perform hello following steps:**</span></span>

1. <span data-ttu-id="1ad5e-197">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1ad5e-199">Na lista de aplicativos hello, selecione **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-199">In hello applications list, select **Intralinks**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="1ad5e-201">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1ad5e-203">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-203">Click **Add** button.</span></span> <span data-ttu-id="1ad5e-204">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1ad5e-206">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1ad5e-207">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1ad5e-208">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="1ad5e-209">Adicionar o aplicativo Intralinks VIA ou Elite</span><span class="sxs-lookup"><span data-stu-id="1ad5e-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="1ad5e-210">Usa Intralinks Olá mesma plataforma de identidade SSO para todos os outros aplicativos Intralinks excluindo aplicativo Nexus de negócio.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-210">Intralinks uses hello same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="1ad5e-211">Para que se planejar toouse qualquer outro aplicativo de Intralinks, em seguida, primeiro é necessário tooconfigure SSO para um aplicativo primário Intralinks usando Olá procedimento descrito acima.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-211">So if you plan toouse any other Intralinks application then first you have tooconfigure SSO for one Primary Intralinks application using hello procedure described above.</span></span>

<span data-ttu-id="1ad5e-212">Depois que você pode seguir Olá abaixo procedimento tooadd outro aplicativo Intralinks em seu locatário que pode aproveitar esse aplicativo primário para o SSO.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-212">After that you can follow hello below procedure tooadd another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="1ad5e-213">Este recurso está disponível apenas clientes de SKU do tooAzure AD Premium e não está disponível para clientes gratuito ou básico de SKU.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-213">This feature is available only tooAzure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="1ad5e-214">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-214">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="1ad5e-216">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-216">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1ad5e-217">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-217">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1ad5e-219">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-219">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1ad5e-221">Na caixa de pesquisa hello, digite **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-221">In hello search box, type **Intralinks**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="1ad5e-223">Em **Intralinks Adicionar aplicativo** executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ad5e-223">On **Intralinks Add app** perform hello following steps:</span></span>

    ![Adicionar o aplicativo Intralinks VIA ou Elite](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="1ad5e-225">a.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-225">a.</span></span> <span data-ttu-id="1ad5e-226">Em **nome** caixa de texto, digite o nome apropriado do aplicativo hello, por exemplo, **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-226">In **Name** textbox, enter appropriate name of hello application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="1ad5e-227">b.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-227">b.</span></span> <span data-ttu-id="1ad5e-228">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="1ad5e-229">Em Olá portal do Azure, Olá **Intralinks** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-229">In hello Azure portal, on hello **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

7. <span data-ttu-id="1ad5e-231">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **logon vinculado**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-231">On hello **Single sign-on** dialog, select **Mode** as   **Linked Sign-on**.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="1ad5e-233">Obter URL do SSO iniciado Olá Olá SP de [Intralinks equipe](https://www.intralinks.com/contact-1) para Olá outro aplicativo Intralinks e insira-a na **configurar URL de logon** conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-233">Get hello hello SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for hello other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="1ad5e-235">Na caixa de texto de URL de entrada hello, digite Olá URL usado pelo seu aplicativo de Intralinks tooyour toosign em usuários usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ad5e-235">In hello Sign On URL textbox, type hello URL used by your users toosign-on tooyour Intralinks application using hello following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="1ad5e-236">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1ad5e-236">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="1ad5e-238">Atribuir Olá aplicativo toouser ou grupos, conforme mostrado na seção de saudação  **[usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-238">Assign hello application toouser or groups as shown in hello section **[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="1ad5e-239">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1ad5e-239">Testing single sign-on</span></span>

<span data-ttu-id="1ad5e-240">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-240">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1ad5e-241">Quando você clica em Olá Intralinks bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Intralinks aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1ad5e-241">When you click hello Intralinks tile in hello Access Panel, you should get automatically signed-on tooyour Intralinks application.</span></span>
<span data-ttu-id="1ad5e-242">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1ad5e-242">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1ad5e-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1ad5e-243">Additional resources</span></span>

* [<span data-ttu-id="1ad5e-244">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1ad5e-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1ad5e-245">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1ad5e-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

