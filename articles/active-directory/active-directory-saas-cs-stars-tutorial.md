---
title: "Tutorial: integração do Azure Active Directory ao CS Stars | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o CS estrelas."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5704d151-afb8-40a4-b286-8bacd4f279ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: d84533e8a7e9bca2f7bdf4be7f3050bca2f18496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cs-stars"></a><span data-ttu-id="3c468-103">Tutorial: integração do Active Directory do Azure ao CS Stars</span><span class="sxs-lookup"><span data-stu-id="3c468-103">Tutorial: Azure Active Directory integration with CS Stars</span></span>

<span data-ttu-id="3c468-104">Neste tutorial, você aprenderá como toointegrate CS estrelas com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="3c468-104">In this tutorial, you learn how toointegrate CS Stars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3c468-105">Integrando CS estrelas com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c468-105">Integrating CS Stars with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3c468-106">Você pode controlar no AD do Azure que tenha acesso tooCS estrelas</span><span class="sxs-lookup"><span data-stu-id="3c468-106">You can control in Azure AD who has access tooCS Stars</span></span>
- <span data-ttu-id="3c468-107">Você pode habilitar seu usuários tooautomatically obter estrelas tooCS conectado (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c468-107">You can enable your users tooautomatically get signed-on tooCS Stars (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3c468-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3c468-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3c468-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3c468-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3c468-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3c468-110">Prerequisites</span></span>

<span data-ttu-id="3c468-111">tooconfigure integração do AD do Azure com estrelas CS, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c468-111">tooconfigure Azure AD integration with CS Stars, you need hello following items:</span></span>

- <span data-ttu-id="3c468-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c468-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3c468-113">Uma assinatura do CS Stars habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="3c468-113">A CS Stars single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3c468-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3c468-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3c468-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3c468-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3c468-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3c468-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3c468-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3c468-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3c468-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3c468-118">Scenario description</span></span>
<span data-ttu-id="3c468-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3c468-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3c468-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="3c468-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3c468-121">Adicionando CS estrelas da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3c468-121">Adding CS Stars from hello gallery</span></span>
2. <span data-ttu-id="3c468-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c468-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cs-stars-from-hello-gallery"></a><span data-ttu-id="3c468-123">Adicionando CS estrelas da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3c468-123">Adding CS Stars from hello gallery</span></span>
<span data-ttu-id="3c468-124">integração de saudação tooconfigure de estrelas de CS no AD do Azure, você precisa tooadd CS estrelas na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3c468-124">tooconfigure hello integration of CS Stars into Azure AD, you need tooadd CS Stars from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3c468-125">**tooadd estrelas CS da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3c468-125">**tooadd CS Stars from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c468-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3c468-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3c468-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3c468-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3c468-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3c468-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3c468-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c468-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3c468-133">Na caixa de pesquisa hello, digite **CS estrelas**.</span><span class="sxs-lookup"><span data-stu-id="3c468-133">In hello search box, type **CS Stars**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_search.png)

5. <span data-ttu-id="3c468-135">No painel de resultados de saudação, selecione **CS estrelas**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3c468-135">In hello results panel, select **CS Stars**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3c468-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c468-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3c468-138">Nesta seção, você configurará e testará o logon único do Azure AD com o CS Stars, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3c468-138">In this section, you configure and test Azure AD single sign-on with CS Stars based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3c468-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em CS estrelas é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c468-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in CS Stars is tooa user in Azure AD.</span></span> <span data-ttu-id="3c468-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em CS estrelas precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="3c468-140">In other words, a link relationship between an Azure AD user and hello related user in CS Stars needs toobe established.</span></span>

<span data-ttu-id="3c468-141">CS estrelas, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c468-141">In CS Stars, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="3c468-142">tooconfigure e teste de logon único do AD do Azure com estrelas CS, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c468-142">tooconfigure and test Azure AD single sign-on with CS Stars, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3c468-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3c468-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3c468-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3c468-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3c468-145">**[Criar um usuário de teste de estrelas de CS](#creating-a-cs-stars-test-user)**  -toohave um equivalente do Britta Simon em CS estrelas que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="3c468-145">**[Creating a CS Stars test user](#creating-a-cs-stars-test-user)** - toohave a counterpart of Britta Simon in CS Stars that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3c468-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="3c468-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3c468-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="3c468-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3c468-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c468-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3c468-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo CS estrelas.</span><span class="sxs-lookup"><span data-stu-id="3c468-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your CS Stars application.</span></span>

<span data-ttu-id="3c468-150">**tooconfigure AD do Azure-logon único com estrelas CS, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3c468-150">**tooconfigure Azure AD single sign-on with CS Stars, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c468-151">Em Olá portal do Azure, Olá **CS estrelas** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="3c468-151">In hello Azure portal, on hello **CS Stars** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3c468-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="3c468-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_samlbase.png)

3. <span data-ttu-id="3c468-155">Em Olá **URLs e domínio do CS estrelas** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c468-155">On hello **CS Stars Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_url.png)

    <span data-ttu-id="3c468-157">a.</span><span class="sxs-lookup"><span data-stu-id="3c468-157">a.</span></span> <span data-ttu-id="3c468-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.csstars.com/enterprise/default.cmdx?ssoclient=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="3c468-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.csstars.com/enterprise/default.cmdx?ssoclient=<uniqueid>`</span></span>

    <span data-ttu-id="3c468-159">b.</span><span class="sxs-lookup"><span data-stu-id="3c468-159">b.</span></span> <span data-ttu-id="3c468-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.csstars.com/enterprise/`</span><span class="sxs-lookup"><span data-stu-id="3c468-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.csstars.com/enterprise/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3c468-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="3c468-161">These values are not real.</span></span> <span data-ttu-id="3c468-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="3c468-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3c468-163">Entre em contato com [equipe de suporte do cliente de estrelas de CS](http://www.marshclearsight.com/support/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="3c468-163">Contact [CS Stars Client support team](http://www.marshclearsight.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="3c468-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3c468-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_certificate.png) 

5. <span data-ttu-id="3c468-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3c468-166">Click **Save** button.</span></span>

    <span data-ttu-id="3c468-167">![Configurar Logon Único](./media/active-directory-saas-cs-stars-tutorial/tutorial_general_400.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="3c468-167">![Configure Single Sign-On](./media/active-directory-saas-cs-stars-tutorial/tutorial_general_400.png) 
<CS></span></span>
6. <span data-ttu-id="3c468-168">tooconfigure logon único no **CS estrelas** lado, você precisa toosend Olá baixado **Metadata XML** muito[equipe de suporte de CS estrelas](http://www.marshclearsight.com/support/).</span><span class="sxs-lookup"><span data-stu-id="3c468-168">tooconfigure single sign-on on **CS Stars** side, you need toosend hello downloaded **Metadata XML** too[CS Stars support team](http://www.marshclearsight.com/support/).</span></span> 
<CE>

> [!TIP]
> <span data-ttu-id="3c468-169">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="3c468-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3c468-170">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="3c468-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3c468-171">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3c468-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3c468-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c468-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="3c468-173">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3c468-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3c468-175">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3c468-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c468-176">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3c468-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3c468-178">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3c468-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3c468-180">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c468-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3c468-182">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3c468-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3c468-184">a.</span><span class="sxs-lookup"><span data-stu-id="3c468-184">a.</span></span> <span data-ttu-id="3c468-185">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3c468-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3c468-186">b.</span><span class="sxs-lookup"><span data-stu-id="3c468-186">b.</span></span> <span data-ttu-id="3c468-187">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3c468-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3c468-188">c.</span><span class="sxs-lookup"><span data-stu-id="3c468-188">c.</span></span> <span data-ttu-id="3c468-189">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="3c468-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3c468-190">d.</span><span class="sxs-lookup"><span data-stu-id="3c468-190">d.</span></span> <span data-ttu-id="3c468-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3c468-191">Click **Create**.</span></span>
 
### <a name="creating-a-cs-stars-test-user"></a><span data-ttu-id="3c468-192">Criando um usuário de teste CS Stars</span><span class="sxs-lookup"><span data-stu-id="3c468-192">Creating a CS Stars test user</span></span>

<span data-ttu-id="3c468-193">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no CS estrelas.</span><span class="sxs-lookup"><span data-stu-id="3c468-193">hello objective of this section is toocreate a user called Britta Simon in CS Stars.</span></span>

<span data-ttu-id="3c468-194">tooget um usuário criado no estrelas CS, você precisa toocontact seu [equipe de suporte de CS estrelas](http://www.marshclearsight.com/support/).</span><span class="sxs-lookup"><span data-stu-id="3c468-194">tooget a user created in CS Stars, you need toocontact your [CS Stars support team](http://www.marshclearsight.com/support/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3c468-195">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3c468-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3c468-196">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCS estrelas.</span><span class="sxs-lookup"><span data-stu-id="3c468-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCS Stars.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3c468-198">**tooassign Britta Simon tooCS estrelas, executar Olá seguintes etapas:**</span><span class="sxs-lookup"><span data-stu-id="3c468-198">**tooassign Britta Simon tooCS Stars, perform hello following steps:**</span></span>

1. <span data-ttu-id="3c468-199">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3c468-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3c468-201">Na lista de aplicativos hello, selecione **CS estrelas**.</span><span class="sxs-lookup"><span data-stu-id="3c468-201">In hello applications list, select **CS Stars**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_app.png) 

3. <span data-ttu-id="3c468-203">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3c468-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3c468-205">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3c468-205">Click **Add** button.</span></span> <span data-ttu-id="3c468-206">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c468-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3c468-208">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c468-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3c468-209">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c468-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3c468-210">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3c468-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3c468-211">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3c468-211">Testing single sign-on</span></span>

<span data-ttu-id="3c468-212">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="3c468-212">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  
<span data-ttu-id="3c468-213">Quando você clica em Olá CS estrelas bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo CS estrelas.</span><span class="sxs-lookup"><span data-stu-id="3c468-213">When you click hello CS Stars tile in hello Access Panel, you should get automatically signed-on tooyour CS Stars application.</span></span>
 

## <a name="additional-resources"></a><span data-ttu-id="3c468-214">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3c468-214">Additional resources</span></span>

* [<span data-ttu-id="3c468-215">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3c468-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3c468-216">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3c468-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_203.png

