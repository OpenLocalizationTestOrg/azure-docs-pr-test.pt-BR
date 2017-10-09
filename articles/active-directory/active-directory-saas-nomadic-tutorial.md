---
title: "Tutorial: integração do Azure Active Directory ao Nomadic | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Nomadic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 13d02b1c-d98a-40b1-824f-afa45a2deb6a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 8c1d3e350ce03c373cf475b2786ec299a7ce5f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nomadic"></a><span data-ttu-id="5f09f-103">Tutorial: Integração do Azure Active Directory com o Nomadic</span><span class="sxs-lookup"><span data-stu-id="5f09f-103">Tutorial: Azure Active Directory integration with Nomadic</span></span>

<span data-ttu-id="5f09f-104">Neste tutorial, você aprenderá como toointegrate Nomadic com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="5f09f-104">In this tutorial, you learn how toointegrate Nomadic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5f09f-105">Integrando Nomadic com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f09f-105">Integrating Nomadic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5f09f-106">Você pode controlar no AD do Azure que tenha acesso tooNomadic.</span><span class="sxs-lookup"><span data-stu-id="5f09f-106">You can control in Azure AD who has access tooNomadic.</span></span>
- <span data-ttu-id="5f09f-107">Você pode habilitar seu usuários tooautomatically get conectado tooNomadic (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f09f-107">You can enable your users tooautomatically get signed-on tooNomadic (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5f09f-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f09f-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="5f09f-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5f09f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f09f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5f09f-110">Prerequisites</span></span>

<span data-ttu-id="5f09f-111">tooconfigure integração do AD do Azure com Nomadic, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f09f-111">tooconfigure Azure AD integration with Nomadic, you need hello following items:</span></span>

- <span data-ttu-id="5f09f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5f09f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5f09f-113">Uma assinatura do Nomadic habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="5f09f-113">A Nomadic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5f09f-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5f09f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5f09f-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5f09f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5f09f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5f09f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5f09f-117">Se você não tiver um ambiente de avaliação do Azure AD, você poderá [obter uma versão de avaliação de um mês aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5f09f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5f09f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5f09f-118">Scenario description</span></span>
<span data-ttu-id="5f09f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5f09f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5f09f-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="5f09f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5f09f-121">Adicionar Nomadic da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5f09f-121">Add Nomadic from hello gallery</span></span>
2. <span data-ttu-id="5f09f-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f09f-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-nomadic-from-hello-gallery"></a><span data-ttu-id="5f09f-123">Adicionar Nomadic da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5f09f-123">Add Nomadic from hello gallery</span></span>
<span data-ttu-id="5f09f-124">integração de saudação tooconfigure de Nomadic no AD do Azure, você precisa tooadd Nomadic da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5f09f-124">tooconfigure hello integration of Nomadic into Azure AD, you need tooadd Nomadic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5f09f-125">**tooadd Nomadic da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5f09f-125">**tooadd Nomadic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f09f-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5f09f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="5f09f-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5f09f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5f09f-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5f09f-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="5f09f-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5f09f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="5f09f-133">Na caixa de pesquisa hello, digite **Nomadic**, selecione **Nomadic** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5f09f-133">In hello search box, type **Nomadic**, select **Nomadic** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Nômades na lista de resultados de saudação](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5f09f-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f09f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5f09f-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Nomadic, com base em um usuário de teste chamado “Britta Simon”.</span><span class="sxs-lookup"><span data-stu-id="5f09f-136">In this section, you configure and test Azure AD single sign-on with Nomadic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5f09f-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Nomadic é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f09f-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nomadic is tooa user in Azure AD.</span></span> <span data-ttu-id="5f09f-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Nomadic precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="5f09f-138">In other words, a link relationship between an Azure AD user and hello related user in Nomadic needs toobe established.</span></span>

<span data-ttu-id="5f09f-139">Nomadic, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f09f-139">In Nomadic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5f09f-140">tooconfigure e teste de logon único do AD do Azure com Nomadic, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f09f-140">tooconfigure and test Azure AD single sign-on with Nomadic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5f09f-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5f09f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5f09f-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5f09f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5f09f-143">**[Criar um usuário de teste nômades](#create-a-nomadic-test-user)**  -toohave um equivalente do Britta Simon em Nomadic é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="5f09f-143">**[Create a Nomadic test user](#create-a-nomadic-test-user)** - toohave a counterpart of Britta Simon in Nomadic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5f09f-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="5f09f-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5f09f-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="5f09f-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5f09f-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f09f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5f09f-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo nômades.</span><span class="sxs-lookup"><span data-stu-id="5f09f-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nomadic application.</span></span>

<span data-ttu-id="5f09f-148">**tooconfigure AD do Azure-logon único com Nomadic, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5f09f-148">**tooconfigure Azure AD single sign-on with Nomadic, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f09f-149">Em Olá portal do Azure, Olá **Nomadic** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="5f09f-149">In hello Azure portal, on hello **Nomadic** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="5f09f-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="5f09f-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_samlbase.png)

3. <span data-ttu-id="5f09f-153">Em Olá **nômades de domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f09f-153">On hello **Nomadic Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do Nomadic](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_url.png)

    <span data-ttu-id="5f09f-155">a.</span><span class="sxs-lookup"><span data-stu-id="5f09f-155">a.</span></span> <span data-ttu-id="5f09f-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company name>.nomadic.fm/signin`</span><span class="sxs-lookup"><span data-stu-id="5f09f-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company name>.nomadic.fm/signin`</span></span>

    <span data-ttu-id="5f09f-157">b.</span><span class="sxs-lookup"><span data-stu-id="5f09f-157">b.</span></span> <span data-ttu-id="5f09f-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir: `https://<company name>.nomadic.fm/auth/saml2/sp`,`https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span><span class="sxs-lookup"><span data-stu-id="5f09f-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.nomadic.fm/auth/saml2/sp`, `https://<company name>.staging.nomadic.fm/auth/saml2/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5f09f-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="5f09f-159">These values are not real.</span></span> <span data-ttu-id="5f09f-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="5f09f-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5f09f-161">Entre em contato com [equipe de suporte do cliente nômades](mailto:help@nomadic.fm) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="5f09f-161">Contact [Nomadic Client support team](mailto:help@nomadic.fm) tooget these values.</span></span> 
 


4. <span data-ttu-id="5f09f-162">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5f09f-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_certificate.png) 

5. <span data-ttu-id="5f09f-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5f09f-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-nomadic-tutorial/tutorial_general_400.png)

6.  <span data-ttu-id="5f09f-166">tooget SSO configurado para o seu aplicativo, entre em contato com [a equipe de suporte nômades](mailto:help@nomadic.fm) e fornecê-los com hello baixado **metadados**.</span><span class="sxs-lookup"><span data-stu-id="5f09f-166">tooget SSO configured for your application, contact [Nomadic support team](mailto:help@nomadic.fm) and provide them with hello downloaded **metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="5f09f-167">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="5f09f-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5f09f-168">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="5f09f-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5f09f-169">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5f09f-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5f09f-170">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f09f-170">Create an Azure AD test user</span></span>

<span data-ttu-id="5f09f-171">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5f09f-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="5f09f-173">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5f09f-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f09f-174">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="5f09f-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-nomadic-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5f09f-176">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="5f09f-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-nomadic-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5f09f-178">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5f09f-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-nomadic-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5f09f-180">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5f09f-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-nomadic-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5f09f-182">a.</span><span class="sxs-lookup"><span data-stu-id="5f09f-182">a.</span></span> <span data-ttu-id="5f09f-183">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5f09f-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5f09f-184">b.</span><span class="sxs-lookup"><span data-stu-id="5f09f-184">b.</span></span> <span data-ttu-id="5f09f-185">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5f09f-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="5f09f-186">c.</span><span class="sxs-lookup"><span data-stu-id="5f09f-186">c.</span></span> <span data-ttu-id="5f09f-187">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="5f09f-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="5f09f-188">d.</span><span class="sxs-lookup"><span data-stu-id="5f09f-188">d.</span></span> <span data-ttu-id="5f09f-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5f09f-189">Click **Create**.</span></span>
 
### <a name="create-a-nomadic-test-user"></a><span data-ttu-id="5f09f-190">Criar um usuário de teste do Nomadic</span><span class="sxs-lookup"><span data-stu-id="5f09f-190">Create a Nomadic test user</span></span>

<span data-ttu-id="5f09f-191">Nesta seção, você criará um usuário chamado Britta Simon no Nomadic.</span><span class="sxs-lookup"><span data-stu-id="5f09f-191">In this section, you create a user called Britta Simon in Nomadic.</span></span> <span data-ttu-id="5f09f-192">Trabalhe com [a equipe de suporte nômades](mailto:help@nomadic.fm) tooadd usuários de saudação na plataforma nômades hello.</span><span class="sxs-lookup"><span data-stu-id="5f09f-192">Please work with [Nomadic support team](mailto:help@nomadic.fm) tooadd hello users in hello Nomadic platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5f09f-193">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5f09f-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5f09f-194">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooNomadic.</span><span class="sxs-lookup"><span data-stu-id="5f09f-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNomadic.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="5f09f-196">**tooassign Britta Simon tooNomadic, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5f09f-196">**tooassign Britta Simon tooNomadic, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f09f-197">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5f09f-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5f09f-199">Na lista de aplicativos hello, selecione **Nomadic**.</span><span class="sxs-lookup"><span data-stu-id="5f09f-199">In hello applications list, select **Nomadic**.</span></span>

    ![Olá Nomadic link na lista de aplicativos Olá](./media/active-directory-saas-nomadic-tutorial/tutorial_nomadic_app.png)  

3. <span data-ttu-id="5f09f-201">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5f09f-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="5f09f-203">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5f09f-203">Click **Add** button.</span></span> <span data-ttu-id="5f09f-204">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5f09f-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="5f09f-206">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f09f-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5f09f-207">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5f09f-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5f09f-208">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5f09f-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5f09f-209">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="5f09f-209">Test single sign-on</span></span>

<span data-ttu-id="5f09f-210">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="5f09f-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5f09f-211">Quando você clica em bloco nômades Olá em Olá painel de acesso, você deverá obter o aplicativo nômades tooyour automaticamente conectado em.</span><span class="sxs-lookup"><span data-stu-id="5f09f-211">When you click hello Nomadic tile in hello Access Panel, you should get automatically signed-on tooyour Nomadic application.</span></span>
<span data-ttu-id="5f09f-212">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5f09f-212">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5f09f-213">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5f09f-213">Additional resources</span></span>

* [<span data-ttu-id="5f09f-214">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5f09f-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5f09f-215">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5f09f-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nomadic-tutorial/tutorial_general_203.png

