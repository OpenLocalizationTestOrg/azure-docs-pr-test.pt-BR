---
title: "Tutorial: Integração do Azure Active Directory ao Capriza Platform | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e plataforma Capriza."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 48d92247-f00a-47b9-8d4e-137028d9e200
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 1c4adb737bb5ba4690bbf74688010238c5c83f3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-capriza-platform"></a><span data-ttu-id="82e64-103">Tutorial: Integração do Azure Active Directory ao Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="82e64-103">Tutorial: Azure Active Directory integration with Capriza Platform</span></span>

<span data-ttu-id="82e64-104">Neste tutorial, você aprenderá como toointegrate Capriza plataforma com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="82e64-104">In this tutorial, you learn how toointegrate Capriza Platform with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="82e64-105">Integração de plataforma Capriza com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="82e64-105">Integrating Capriza Platform with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="82e64-106">Você pode controlar no AD do Azure que tenha acesso tooCapriza plataforma</span><span class="sxs-lookup"><span data-stu-id="82e64-106">You can control in Azure AD who has access tooCapriza Platform</span></span>
- <span data-ttu-id="82e64-107">Você pode habilitar seu usuários tooautomatically get conectado tooCapriza plataforma (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="82e64-107">You can enable your users tooautomatically get signed-on tooCapriza Platform (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="82e64-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="82e64-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="82e64-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="82e64-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82e64-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="82e64-110">Prerequisites</span></span>

<span data-ttu-id="82e64-111">tooconfigure integração do AD do Azure com a plataforma de Capriza, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="82e64-111">tooconfigure Azure AD integration with Capriza Platform, you need hello following items:</span></span>

- <span data-ttu-id="82e64-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="82e64-112">An Azure AD subscription</span></span>
- <span data-ttu-id="82e64-113">Uma assinatura habilitada para logon único do Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="82e64-113">A Capriza Platform single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="82e64-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="82e64-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="82e64-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="82e64-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="82e64-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="82e64-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="82e64-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="82e64-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="82e64-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="82e64-118">Scenario description</span></span>
<span data-ttu-id="82e64-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="82e64-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="82e64-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="82e64-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="82e64-121">Adicionando Capriza plataforma da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="82e64-121">Adding Capriza Platform from hello gallery</span></span>
2. <span data-ttu-id="82e64-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="82e64-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-capriza-platform-from-hello-gallery"></a><span data-ttu-id="82e64-123">Adicionando Capriza plataforma da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="82e64-123">Adding Capriza Platform from hello gallery</span></span>
<span data-ttu-id="82e64-124">integração de saudação tooconfigure da plataforma Capriza no AD do Azure, você precisa tooadd Capriza plataforma da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="82e64-124">tooconfigure hello integration of Capriza Platform into Azure AD, you need tooadd Capriza Platform from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="82e64-125">**tooadd Capriza plataforma da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="82e64-125">**tooadd Capriza Platform from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="82e64-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="82e64-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="82e64-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="82e64-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="82e64-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="82e64-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="82e64-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="82e64-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="82e64-133">Na caixa de pesquisa hello, digite **Capriza plataforma**.</span><span class="sxs-lookup"><span data-stu-id="82e64-133">In hello search box, type **Capriza Platform**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_search.png)

5. <span data-ttu-id="82e64-135">No painel de resultados de saudação, selecione **Capriza plataforma**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="82e64-135">In hello results panel, select **Capriza Platform**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="82e64-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="82e64-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="82e64-138">Nesta seção, você configura e testa o logon único do Azure AD com o Capriza Platform, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="82e64-138">In this section, you configure and test Azure AD single sign-on with Capriza Platform based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="82e64-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na plataforma de Capriza é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="82e64-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Capriza Platform is tooa user in Azure AD.</span></span> <span data-ttu-id="82e64-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na plataforma Capriza precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="82e64-140">In other words, a link relationship between an Azure AD user and hello related user in Capriza Platform needs toobe established.</span></span>

<span data-ttu-id="82e64-141">Na plataforma de Capriza, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="82e64-141">In Capriza Platform, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="82e64-142">tooconfigure e teste de logon único do AD do Azure com a plataforma de Capriza, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="82e64-142">tooconfigure and test Azure AD single sign-on with Capriza Platform, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="82e64-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="82e64-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="82e64-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82e64-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="82e64-145">**[Criar um usuário de teste de plataforma Capriza](#creating-a-capriza-platform-test-user)**  -toohave um equivalente do Britta Simon na plataforma de Capriza toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="82e64-145">**[Creating a Capriza Platform test user](#creating-a-capriza-platform-test-user)** - toohave a counterpart of Britta Simon in Capriza Platform that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="82e64-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="82e64-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="82e64-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="82e64-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="82e64-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="82e64-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="82e64-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de plataforma Capriza.</span><span class="sxs-lookup"><span data-stu-id="82e64-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Capriza Platform application.</span></span>

<span data-ttu-id="82e64-150">**tooconfigure AD do Azure-logon único com a plataforma de Capriza executar Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="82e64-150">**tooconfigure Azure AD single sign-on with Capriza Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="82e64-151">Em Olá portal do Azure, Olá **Capriza plataforma** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="82e64-151">In hello Azure portal, on hello **Capriza Platform** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="82e64-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="82e64-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_samlbase.png)

3. <span data-ttu-id="82e64-155">Em Olá **Capriza plataforma de domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="82e64-155">On hello **Capriza Platform Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_url.png)

    <span data-ttu-id="82e64-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.capriza.com/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="82e64-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.capriza.com/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="82e64-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="82e64-158">This value is not real.</span></span> <span data-ttu-id="82e64-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="82e64-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="82e64-160">Entre em contato com [equipe de suporte de cliente da plataforma Capriza](mailTo:support@capriza.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="82e64-160">Contact [Capriza Platform Client support team](mailTo:support@capriza.com) tooget this value.</span></span> 

4. <span data-ttu-id="82e64-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="82e64-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_certificate.png) 

5. <span data-ttu-id="82e64-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="82e64-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-capriza-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="82e64-165">Em Olá **Capriza plataforma configuração** seção, clique em **configurar Capriza plataforma** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="82e64-165">On hello **Capriza Platform Configuration** section, click **Configure Capriza Platform** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="82e64-166">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="82e64-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_configure.png) 

7. <span data-ttu-id="82e64-168">tooconfigure logon único no **Capriza plataforma** lado, você precisa toosend Olá baixado **certificado**, **URL de logout**, **ID da entidade SAML** e **Single Sign-On URL do serviço SAML** muito[equipe de suporte de plataforma Capriza](mailTo:support@capriza.com).</span><span class="sxs-lookup"><span data-stu-id="82e64-168">tooconfigure single sign-on on **Capriza Platform** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Capriza Platform support team](mailTo:support@capriza.com).</span></span> <span data-ttu-id="82e64-169">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="82e64-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="82e64-170">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="82e64-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="82e64-171">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="82e64-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="82e64-172">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="82e64-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="82e64-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="82e64-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="82e64-174">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="82e64-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="82e64-176">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="82e64-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="82e64-177">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="82e64-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-capriza-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="82e64-179">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="82e64-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-capriza-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="82e64-181">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="82e64-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-capriza-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="82e64-183">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="82e64-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-capriza-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="82e64-185">a.</span><span class="sxs-lookup"><span data-stu-id="82e64-185">a.</span></span> <span data-ttu-id="82e64-186">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="82e64-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="82e64-187">b.</span><span class="sxs-lookup"><span data-stu-id="82e64-187">b.</span></span> <span data-ttu-id="82e64-188">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="82e64-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="82e64-189">c.</span><span class="sxs-lookup"><span data-stu-id="82e64-189">c.</span></span> <span data-ttu-id="82e64-190">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="82e64-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="82e64-191">d.</span><span class="sxs-lookup"><span data-stu-id="82e64-191">d.</span></span> <span data-ttu-id="82e64-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="82e64-192">Click **Create**.</span></span>
 
### <a name="creating-a-capriza-platform-test-user"></a><span data-ttu-id="82e64-193">Criando um usuário de teste do Capriza Platform</span><span class="sxs-lookup"><span data-stu-id="82e64-193">Creating a Capriza Platform test user</span></span>

<span data-ttu-id="82e64-194">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Capriza.</span><span class="sxs-lookup"><span data-stu-id="82e64-194">hello objective of this section is toocreate a user called Britta Simon in Capriza.</span></span> <span data-ttu-id="82e64-195">O Capriza dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="82e64-195">Capriza supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="82e64-196">**Verifique se o nome de domínio está configurado no Capriza para o provisionamento de usuário. Depois que Olá somente o provisionamento de usuário just-in-time funcione.**</span><span class="sxs-lookup"><span data-stu-id="82e64-196">**Please make sure that your domain name is configured with Capriza for user provisioning. After that only hello just-in-time user provisioning will work.**</span></span>

<span data-ttu-id="82e64-197">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="82e64-197">There is no action item for you in this section.</span></span> <span data-ttu-id="82e64-198">Será criado um novo usuário durante uma tentativa tooaccess Capriza se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="82e64-198">A new user will be created during an attempt tooaccess Capriza if it doesn't exist yet.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="82e64-199">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="82e64-199">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="82e64-200">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCapriza plataforma.</span><span class="sxs-lookup"><span data-stu-id="82e64-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCapriza Platform.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="82e64-202">**tooassign Britta Simon tooCapriza plataforma, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="82e64-202">**tooassign Britta Simon tooCapriza Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="82e64-203">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="82e64-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="82e64-205">Na lista de aplicativos hello, selecione **Capriza plataforma**.</span><span class="sxs-lookup"><span data-stu-id="82e64-205">In hello applications list, select **Capriza Platform**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-capriza-tutorial/tutorial_caprizaplatform_app.png) 

3. <span data-ttu-id="82e64-207">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="82e64-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="82e64-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="82e64-209">Click **Add** button.</span></span> <span data-ttu-id="82e64-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="82e64-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="82e64-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="82e64-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="82e64-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="82e64-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="82e64-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="82e64-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="82e64-215">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="82e64-215">Testing single sign-on</span></span>

<span data-ttu-id="82e64-216">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="82e64-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="82e64-217">Quando você clica em Olá Capriza plataforma bloco no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Capriza aplicativo.</span><span class="sxs-lookup"><span data-stu-id="82e64-217">When you click hello Capriza Platform tile in hello Access Panel, you should get automatically signed-on tooyour Capriza application.</span></span> <span data-ttu-id="82e64-218">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="82e64-218">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="82e64-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="82e64-219">Additional resources</span></span>

* [<span data-ttu-id="82e64-220">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="82e64-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="82e64-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="82e64-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-capriza-tutorial/tutorial_general_203.png

