---
title: "Tutorial: Integração do Azure Active Directory ao 15Five | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e 15Five."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2fb301c2-7d7a-4046-8ee1-7dc9e7684806
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 9e531615c16331ce000e285d13d9adce13735a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-15five"></a><span data-ttu-id="c7cac-103">Tutorial: Integração do Active Directory do Azure ao 15Five</span><span class="sxs-lookup"><span data-stu-id="c7cac-103">Tutorial: Azure Active Directory integration with 15Five</span></span>

<span data-ttu-id="c7cac-104">Neste tutorial, você aprenderá como toointegrate 15Five com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c7cac-104">In this tutorial, you learn how toointegrate 15Five with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7cac-105">Integrando o 15Five com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7cac-105">Integrating 15Five with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c7cac-106">Você pode controlar no AD do Azure que tenha acesso too15Five</span><span class="sxs-lookup"><span data-stu-id="c7cac-106">You can control in Azure AD who has access too15Five</span></span>
- <span data-ttu-id="c7cac-107">Você pode habilitar seus usuários tooautomatically get conectado too15Five (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7cac-107">You can enable your users tooautomatically get signed-on too15Five (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7cac-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c7cac-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c7cac-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7cac-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7cac-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c7cac-110">Prerequisites</span></span>

<span data-ttu-id="c7cac-111">tooconfigure integração do AD do Azure com o 15Five, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7cac-111">tooconfigure Azure AD integration with 15Five, you need hello following items:</span></span>

- <span data-ttu-id="c7cac-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7cac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7cac-113">Uma assinatura habilitada para logon único do 15Five</span><span class="sxs-lookup"><span data-stu-id="c7cac-113">A 15Five single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7cac-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c7cac-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7cac-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c7cac-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7cac-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c7cac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7cac-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7cac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7cac-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c7cac-118">Scenario description</span></span>
<span data-ttu-id="c7cac-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c7cac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7cac-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c7cac-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7cac-121">Adicionando 15Five da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c7cac-121">Adding 15Five from hello gallery</span></span>
2. <span data-ttu-id="c7cac-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7cac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-15five-from-hello-gallery"></a><span data-ttu-id="c7cac-123">Adicionando 15Five da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c7cac-123">Adding 15Five from hello gallery</span></span>
<span data-ttu-id="c7cac-124">integração de saudação tooconfigure do 15Five no AD do Azure, você precisa 15Five tooadd da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c7cac-124">tooconfigure hello integration of 15Five into Azure AD, you need tooadd 15Five from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c7cac-125">**15Five tooadd da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7cac-125">**tooadd 15Five from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7cac-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c7cac-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c7cac-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c7cac-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c7cac-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7cac-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c7cac-133">Na caixa de pesquisa hello, digite **15Five**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-133">In hello search box, type **15Five**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/tutorial_15five_search.png)

5. <span data-ttu-id="c7cac-135">No painel de resultados de saudação, selecione **15Five**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c7cac-135">In hello results panel, select **15Five**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/tutorial_15five_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7cac-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7cac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7cac-138">Nesta seção, você configurará e testará o logon único do Azure AD com o 15Five, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c7cac-138">In this section, you configure and test Azure AD single sign-on with 15Five based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c7cac-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no 15Five é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7cac-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 15Five is tooa user in Azure AD.</span></span> <span data-ttu-id="c7cac-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no 15Five precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c7cac-140">In other words, a link relationship between an Azure AD user and hello related user in 15Five needs toobe established.</span></span>

<span data-ttu-id="c7cac-141">No 15Five, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7cac-141">In 15Five, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c7cac-142">tooconfigure e teste de logon único do AD do Azure com o 15Five, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7cac-142">tooconfigure and test Azure AD single sign-on with 15Five, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c7cac-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c7cac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c7cac-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7cac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7cac-145">**[Criar um usuário de teste do 15Five](#creating-a-15five-test-user)**  -toohave um equivalente do Britta Simon no 15Five é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c7cac-145">**[Creating a 15Five test user](#creating-a-15five-test-user)** - toohave a counterpart of Britta Simon in 15Five that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7cac-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c7cac-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7cac-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c7cac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7cac-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7cac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7cac-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do 15Five.</span><span class="sxs-lookup"><span data-stu-id="c7cac-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 15Five application.</span></span>

<span data-ttu-id="c7cac-150">**tooconfigure AD do Azure-logon único com o 15Five, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7cac-150">**tooconfigure Azure AD single sign-on with 15Five, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7cac-151">Em Olá portal do Azure, Olá **15Five** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-151">In hello Azure portal, on hello **15Five** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c7cac-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c7cac-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-15five-tutorial/tutorial_15five_samlbase.png)

3. <span data-ttu-id="c7cac-155">Em Olá **15Five domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7cac-155">On hello **15Five Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-15five-tutorial/tutorial_15five_url.png)

    <span data-ttu-id="c7cac-157">a.</span><span class="sxs-lookup"><span data-stu-id="c7cac-157">a.</span></span> <span data-ttu-id="c7cac-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.15five.com`</span><span class="sxs-lookup"><span data-stu-id="c7cac-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.15five.com`</span></span>

    <span data-ttu-id="c7cac-159">b.</span><span class="sxs-lookup"><span data-stu-id="c7cac-159">b.</span></span> <span data-ttu-id="c7cac-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.15five.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="c7cac-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.15five.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7cac-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c7cac-161">These values are not real.</span></span> <span data-ttu-id="c7cac-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="c7cac-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c7cac-163">Entre em contato com [equipe de suporte do 15Five cliente](https://www.15five.com/contact/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="c7cac-163">Contact [15Five Client support team](https://www.15five.com/contact/) tooget these values.</span></span> 
 
4. <span data-ttu-id="c7cac-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c7cac-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-15five-tutorial/tutorial_15five_certificate.png) 

5. <span data-ttu-id="c7cac-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c7cac-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-15five-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7cac-168">tooconfigure logon único no **15Five** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte do 15Five](https://www.15five.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="c7cac-168">tooconfigure single sign-on on **15Five** side, you need toosend hello downloaded **Metadata XML** too[15Five support team](https://www.15five.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="c7cac-169">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c7cac-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c7cac-170">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c7cac-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c7cac-171">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7cac-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7cac-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7cac-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7cac-173">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7cac-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c7cac-175">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7cac-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7cac-176">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c7cac-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7cac-178">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7cac-180">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7cac-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7cac-182">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7cac-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-15five-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7cac-184">a.</span><span class="sxs-lookup"><span data-stu-id="c7cac-184">a.</span></span> <span data-ttu-id="c7cac-185">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7cac-186">b.</span><span class="sxs-lookup"><span data-stu-id="c7cac-186">b.</span></span> <span data-ttu-id="c7cac-187">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c7cac-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7cac-188">c.</span><span class="sxs-lookup"><span data-stu-id="c7cac-188">c.</span></span> <span data-ttu-id="c7cac-189">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c7cac-190">d.</span><span class="sxs-lookup"><span data-stu-id="c7cac-190">d.</span></span> <span data-ttu-id="c7cac-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-191">Click **Create**.</span></span>
 
### <a name="creating-a-15five-test-user"></a><span data-ttu-id="c7cac-192">Criação de um usuário de teste do 15Five</span><span class="sxs-lookup"><span data-stu-id="c7cac-192">Creating a 15Five test user</span></span>

<span data-ttu-id="c7cac-193">tooenable AD do Azure usuários toolog em too15Five, eles devem ser provisionados no 15Five.</span><span class="sxs-lookup"><span data-stu-id="c7cac-193">tooenable Azure AD users toolog in too15Five, they must be provisioned into 15Five.</span></span> <span data-ttu-id="c7cac-194">No caso do 15Five, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="c7cac-194">When 15Five, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="c7cac-195">tooconfigure provisionamento de usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7cac-195">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="c7cac-196">Faça logon no tooyour **15Five** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="c7cac-196">Log in tooyour **15Five** company site as administrator.</span></span>

2. <span data-ttu-id="c7cac-197">Vá muito**gerenciar empresa**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-197">Go too**Manage Company**.</span></span>
   
    <span data-ttu-id="c7cac-198">![Gerenciar Empresa](./media/active-directory-saas-15five-tutorial/IC784675.png "Gerenciar Empresa")</span><span class="sxs-lookup"><span data-stu-id="c7cac-198">![Manage Company](./media/active-directory-saas-15five-tutorial/IC784675.png "Manage Company")</span></span>

3. <span data-ttu-id="c7cac-199">Vá muito**pessoas \> adicionar pessoas**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-199">Go too**People \> Add People**.</span></span>
   
    <span data-ttu-id="c7cac-200">![Pessoas](./media/active-directory-saas-15five-tutorial/IC784676.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="c7cac-200">![People](./media/active-directory-saas-15five-tutorial/IC784676.png "People")</span></span>

4. <span data-ttu-id="c7cac-201">Na seção Adicionar nova pessoa do hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7cac-201">In hello Add New Person section, perform hello following steps:</span></span>
   
    <span data-ttu-id="c7cac-202">![Adicionar Nova Pessoa](./media/active-directory-saas-15five-tutorial/IC784677.png "Adicionar Nova Pessoa")</span><span class="sxs-lookup"><span data-stu-id="c7cac-202">![Add New Person](./media/active-directory-saas-15five-tutorial/IC784677.png "Add New Person")</span></span>
   
    <span data-ttu-id="c7cac-203">a.</span><span class="sxs-lookup"><span data-stu-id="c7cac-203">a.</span></span> <span data-ttu-id="c7cac-204">Saudação de tipo **nome**, **Sobrenome**, **título**, **endereço de Email** de uma conta válida do Active Directory do Azure que você deseja tooprovision em Olá relacionados caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="c7cac-204">Type hello **First Name**, **Last Name**, **Title**, **Email address** of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="c7cac-205">b.</span><span class="sxs-lookup"><span data-stu-id="c7cac-205">b.</span></span> <span data-ttu-id="c7cac-206">Clique em **Concluído**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-206">Click **Done**.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="c7cac-207">Olá conta do AD do Azure detentor recebe um email com uma conta de saudação do link tooconfirm antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="c7cac-207">hello Azure AD account holder receives an email including a link tooconfirm hello account before it becomes active.</span></span>
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c7cac-208">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7cac-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c7cac-209">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso too15Five.</span><span class="sxs-lookup"><span data-stu-id="c7cac-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too15Five.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c7cac-211">**tooassign Britta Simon too15Five, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7cac-211">**tooassign Britta Simon too15Five, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7cac-212">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c7cac-214">Na lista de aplicativos hello, selecione **15Five**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-214">In hello applications list, select **15Five**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-15five-tutorial/tutorial_15five_app.png) 

3. <span data-ttu-id="c7cac-216">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c7cac-218">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c7cac-218">Click **Add** button.</span></span> <span data-ttu-id="c7cac-219">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7cac-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c7cac-221">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7cac-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c7cac-222">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7cac-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7cac-223">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7cac-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7cac-224">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c7cac-224">Testing single sign-on</span></span>

<span data-ttu-id="c7cac-225">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7cac-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c7cac-226">Quando você clica em bloco 15Five Olá Olá painel de acesso, você deve obter a página de logon do aplicativo do 15Five.</span><span class="sxs-lookup"><span data-stu-id="c7cac-226">When you click hello 15Five tile in hello Access Panel, you should get login page of 15Five application.</span></span>
<span data-ttu-id="c7cac-227">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c7cac-227">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c7cac-228">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c7cac-228">Additional resources</span></span>

* [<span data-ttu-id="c7cac-229">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c7cac-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7cac-230">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7cac-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-15five-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-15five-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-15five-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-15five-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-15five-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-15five-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-15five-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-15five-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-15five-tutorial/tutorial_general_203.png

