---
title: "Tutorial: Integração do Azure Active Directory ao Brightspace by Desire2Learn | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Brightspace by Desire2Learn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2d3065b-1f6c-4c45-af78-0d5da3266999
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 99d03dc50defcb291a651a5415e30baab39e1e77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-brightspace-by-desire2learn"></a><span data-ttu-id="111b9-103">Tutorial: Integração do Active Directory do Azure ao Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="111b9-103">Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn</span></span>

<span data-ttu-id="111b9-104">Neste tutorial, você aprenderá como toointegrate Brightspace by Desire2Learn com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="111b9-104">In this tutorial, you learn how toointegrate Brightspace by Desire2Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="111b9-105">Integrando o Brightspace by Desire2Learn com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="111b9-105">Integrating Brightspace by Desire2Learn with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="111b9-106">Você pode controlar no AD do Azure que tenha acesso tooBrightspace pelo Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="111b9-106">You can control in Azure AD who has access tooBrightspace by Desire2Learn</span></span>
- <span data-ttu-id="111b9-107">Você pode habilitar seu usuários tooautomatically get conectado tooBrightspace por Desire2Learn (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="111b9-107">You can enable your users tooautomatically get signed-on tooBrightspace by Desire2Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="111b9-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="111b9-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="111b9-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="111b9-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="111b9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="111b9-110">Prerequisites</span></span>

<span data-ttu-id="111b9-111">tooconfigure integração do AD do Azure com o Brightspace by Desire2Learn, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="111b9-111">tooconfigure Azure AD integration with Brightspace by Desire2Learn, you need hello following items:</span></span>

- <span data-ttu-id="111b9-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="111b9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="111b9-113">Uma assinatura habilitada para logon único do Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="111b9-113">A Brightspace by Desire2Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="111b9-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="111b9-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="111b9-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="111b9-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="111b9-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="111b9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="111b9-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="111b9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="111b9-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="111b9-118">Scenario description</span></span>
<span data-ttu-id="111b9-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="111b9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="111b9-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="111b9-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="111b9-121">Adicionando Brightspace by Desire2Learn da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="111b9-121">Adding Brightspace by Desire2Learn from hello gallery</span></span>
2. <span data-ttu-id="111b9-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="111b9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-brightspace-by-desire2learn-from-hello-gallery"></a><span data-ttu-id="111b9-123">Adicionando Brightspace by Desire2Learn da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="111b9-123">Adding Brightspace by Desire2Learn from hello gallery</span></span>
<span data-ttu-id="111b9-124">integração de saudação tooconfigure do Brightspace by Desire2Learn no AD do Azure, você precisa tooadd Brightspace by Desire2Learn da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="111b9-124">tooconfigure hello integration of Brightspace by Desire2Learn into Azure AD, you need tooadd Brightspace by Desire2Learn from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="111b9-125">**tooadd Brightspace by Desire2Learn da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="111b9-125">**tooadd Brightspace by Desire2Learn from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="111b9-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="111b9-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="111b9-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="111b9-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="111b9-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="111b9-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="111b9-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="111b9-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="111b9-133">Na caixa de pesquisa hello, digite **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="111b9-133">In hello search box, type **Brightspace by Desire2Learn**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_search.png)

5. <span data-ttu-id="111b9-135">No painel de resultados de saudação, selecione **Brightspace by Desire2Learn**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="111b9-135">In hello results panel, select **Brightspace by Desire2Learn**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="111b9-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="111b9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="111b9-138">Nesta seção, você configura e testa o logon único do Azure AD com o Brightspace by Desire2Learn, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="111b9-138">In this section, you configure and test Azure AD single sign-on with Brightspace by Desire2Learn based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="111b9-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Brightspace by Desire2Learn é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="111b9-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Brightspace by Desire2Learn is tooa user in Azure AD.</span></span> <span data-ttu-id="111b9-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Brightspace by Desire2Learn precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="111b9-140">In other words, a link relationship between an Azure AD user and hello related user in Brightspace by Desire2Learn needs toobe established.</span></span>

<span data-ttu-id="111b9-141">No Brightspace by Desire2Learn, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="111b9-141">In Brightspace by Desire2Learn, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="111b9-142">tooconfigure e teste de logon único do AD do Azure com o Brightspace pelo Desire2Learn, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="111b9-142">tooconfigure and test Azure AD single sign-on with Brightspace by Desire2Learn, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="111b9-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="111b9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="111b9-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="111b9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="111b9-145">**[Criando um Brightspace by Desire2Learn testar usuário](#creating-a-brightspace-by-desire2learn-test-user)**  -toohave um equivalente do Britta Simon no Brightspace by Desire2Learn é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="111b9-145">**[Creating a Brightspace by Desire2Learn test user](#creating-a-brightspace-by-desire2learn-test-user)** - toohave a counterpart of Britta Simon in Brightspace by Desire2Learn that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="111b9-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="111b9-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="111b9-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="111b9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="111b9-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="111b9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="111b9-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único do Brightspace por Desire2Learn aplicativo.</span><span class="sxs-lookup"><span data-stu-id="111b9-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Brightspace by Desire2Learn application.</span></span>

<span data-ttu-id="111b9-150">**tooconfigure AD do Azure-logon único com o Brightspace pelo Desire2Learn, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="111b9-150">**tooconfigure Azure AD single sign-on with Brightspace by Desire2Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="111b9-151">Em Olá portal do Azure, Olá **Brightspace by Desire2Learn** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="111b9-151">In hello Azure portal, on hello **Brightspace by Desire2Learn** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="111b9-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="111b9-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_samlbase.png)

3. <span data-ttu-id="111b9-155">Em Olá **Brightspace by Desire2Learn domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="111b9-155">On hello **Brightspace by Desire2Learn Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_url.png)

    <span data-ttu-id="111b9-157">a.</span><span class="sxs-lookup"><span data-stu-id="111b9-157">a.</span></span> <span data-ttu-id="111b9-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="111b9-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.tenants.brightspace.com/samlLogin`|
    | `https://<companyname>.desire2learn.com/shibboleth-sp`|

    <span data-ttu-id="111b9-159">b.</span><span class="sxs-lookup"><span data-stu-id="111b9-159">b.</span></span> <span data-ttu-id="111b9-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span><span class="sxs-lookup"><span data-stu-id="111b9-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="111b9-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="111b9-161">These values are not real.</span></span> <span data-ttu-id="111b9-162">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="111b9-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="111b9-163">Entre em contato com [Brightspace by Desire2Learn a equipe de suporte](https://www.d2l.com/contact/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="111b9-163">Contact [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/) tooget these values.</span></span>
 


4. <span data-ttu-id="111b9-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="111b9-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_certificate.png) 

5. <span data-ttu-id="111b9-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="111b9-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="111b9-168">tooconfigure logon único no **Brightspace by Desire2Learn** lado, você precisa toosend Olá baixado **Metadata XML** muito[Brightspace by Desire2Learn a equipe de suporte](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="111b9-168">tooconfigure single sign-on on **Brightspace by Desire2Learn** side, you need toosend hello downloaded **Metadata XML** too[Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="111b9-169">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="111b9-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="111b9-170">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="111b9-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="111b9-171">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="111b9-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="111b9-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="111b9-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="111b9-173">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="111b9-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="111b9-175">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="111b9-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="111b9-176">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="111b9-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="111b9-178">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="111b9-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="111b9-180">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="111b9-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="111b9-182">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="111b9-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="111b9-184">a.</span><span class="sxs-lookup"><span data-stu-id="111b9-184">a.</span></span> <span data-ttu-id="111b9-185">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="111b9-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="111b9-186">b.</span><span class="sxs-lookup"><span data-stu-id="111b9-186">b.</span></span> <span data-ttu-id="111b9-187">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="111b9-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="111b9-188">c.</span><span class="sxs-lookup"><span data-stu-id="111b9-188">c.</span></span> <span data-ttu-id="111b9-189">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="111b9-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="111b9-190">d.</span><span class="sxs-lookup"><span data-stu-id="111b9-190">d.</span></span> <span data-ttu-id="111b9-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="111b9-191">Click **Create**.</span></span>
 
### <a name="creating-a-brightspace-by-desire2learn-test-user"></a><span data-ttu-id="111b9-192">Criando um usuário de teste do Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="111b9-192">Creating a Brightspace by Desire2Learn test user</span></span>

<span data-ttu-id="111b9-193">Em ordem tooenable AD do Azure usuários toolog no Brightspace by Desire2Learn, eles devem ser provisionados no Brightspace pelo Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="111b9-193">In order tooenable Azure AD users toolog into Brightspace by Desire2Learn, they must be provisioned into Brightspace by Desire2Learn.</span></span>  

<span data-ttu-id="111b9-194">Em caso de saudação do Brightspace by Desire2Learn, contas de usuário de saudação necessário toobe criado por seu [Brightspace by Desire2Learn a equipe de suporte](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="111b9-194">In hello case of Brightspace by Desire2Learn, hello user accounts need toobe created by your [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

>[!NOTE]
><span data-ttu-id="111b9-195">Você pode usar qualquer outra Brightspace pelo Desire2Learn ferramentas de criação de conta de usuário ou APIs fornecidas pelo Brightspace pelo Desire2Learn tooprovision Azure Active Directory as contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="111b9-195">You can use any other Brightspace by Desire2Learn user account creation tools or APIs provided by Brightspace by Desire2Learn tooprovision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="111b9-196">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="111b9-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="111b9-197">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBrightspace por Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="111b9-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBrightspace by Desire2Learn.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="111b9-199">**tooassign Britta Simon tooBrightspace por Desire2Learn, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="111b9-199">**tooassign Britta Simon tooBrightspace by Desire2Learn, perform hello following steps:**</span></span>

1. <span data-ttu-id="111b9-200">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="111b9-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="111b9-202">Na lista de aplicativos hello, selecione **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="111b9-202">In hello applications list, select **Brightspace by Desire2Learn**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_app.png) 

3. <span data-ttu-id="111b9-204">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="111b9-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="111b9-206">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="111b9-206">Click **Add** button.</span></span> <span data-ttu-id="111b9-207">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="111b9-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="111b9-209">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="111b9-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="111b9-210">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="111b9-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="111b9-211">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="111b9-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="111b9-212">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="111b9-212">Testing single sign-on</span></span>

<span data-ttu-id="111b9-213">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="111b9-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="111b9-214">Quando você clica em Olá Brightspace pelo Desire2Learn lado a lado no painel de acesso de saudação, você deve obter automaticamente assinado em tooyour Brightspace pelo Desire2Learn aplicativo.</span><span class="sxs-lookup"><span data-stu-id="111b9-214">When you click hello Brightspace by Desire2Learn tile in hello Access Panel, you should get automatically signed-on tooyour Brightspace by Desire2Learn application.</span></span>
<span data-ttu-id="111b9-215">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="111b9-215">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="111b9-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="111b9-216">Additional resources</span></span>

* [<span data-ttu-id="111b9-217">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="111b9-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="111b9-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="111b9-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_203.png

