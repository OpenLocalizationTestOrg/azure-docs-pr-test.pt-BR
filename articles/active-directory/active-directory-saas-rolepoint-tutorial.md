---
title: "Tutorial: Integração do Azure Active Directory ao RolePoint | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e RolePoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68d37f40-15da-45f5-a9e1-d53f78e786d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: jeedes
ms.openlocfilehash: 8629dd87c17d44ab89251ebbd19156c6d6cbedc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rolepoint"></a><span data-ttu-id="b6227-103">Tutorial: Integração do Azure Active Directory ao RolePoint</span><span class="sxs-lookup"><span data-stu-id="b6227-103">Tutorial: Azure Active Directory integration with RolePoint</span></span>

<span data-ttu-id="b6227-104">Neste tutorial, você aprenderá como toointegrate RolePoint com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="b6227-104">In this tutorial, you learn how toointegrate RolePoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b6227-105">Integrando RolePoint com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="b6227-105">Integrating RolePoint with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b6227-106">Você pode controlar no AD do Azure que tenha acesso tooRolePoint</span><span class="sxs-lookup"><span data-stu-id="b6227-106">You can control in Azure AD who has access tooRolePoint</span></span>
- <span data-ttu-id="b6227-107">Você pode habilitar seu usuários tooautomatically get conectado tooRolePoint (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b6227-107">You can enable your users tooautomatically get signed-on tooRolePoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b6227-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="b6227-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b6227-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b6227-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6227-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b6227-110">Prerequisites</span></span>

<span data-ttu-id="b6227-111">tooconfigure integração do AD do Azure com RolePoint, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="b6227-111">tooconfigure Azure AD integration with RolePoint, you need hello following items:</span></span>

- <span data-ttu-id="b6227-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b6227-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b6227-113">Uma assinatura habilitada para logon único do RolePoint</span><span class="sxs-lookup"><span data-stu-id="b6227-113">A RolePoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b6227-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="b6227-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b6227-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="b6227-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b6227-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="b6227-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b6227-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b6227-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b6227-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="b6227-118">Scenario description</span></span>
<span data-ttu-id="b6227-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="b6227-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b6227-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="b6227-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b6227-121">Adicionando RolePoint da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b6227-121">Adding RolePoint from hello gallery</span></span>
2. <span data-ttu-id="b6227-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b6227-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rolepoint-from-hello-gallery"></a><span data-ttu-id="b6227-123">Adicionando RolePoint da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="b6227-123">Adding RolePoint from hello gallery</span></span>
<span data-ttu-id="b6227-124">integração de saudação tooconfigure de RolePoint no AD do Azure, você precisa tooadd RolePoint da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="b6227-124">tooconfigure hello integration of RolePoint into Azure AD, you need tooadd RolePoint from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b6227-125">**tooadd RolePoint da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b6227-125">**tooadd RolePoint from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b6227-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b6227-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b6227-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="b6227-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b6227-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b6227-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="b6227-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b6227-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="b6227-133">Na caixa de pesquisa hello, digite **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="b6227-133">In hello search box, type **RolePoint**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_search.png)

5. <span data-ttu-id="b6227-135">No painel de resultados de saudação, selecione **RolePoint**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b6227-135">In hello results panel, select **RolePoint**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b6227-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b6227-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b6227-138">Nesta seção, você vai configurar e testar o logon único do Azure AD com o RolePoint com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="b6227-138">In this section, you configure and test Azure AD single sign-on with RolePoint based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b6227-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em RolePoint é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6227-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RolePoint is tooa user in Azure AD.</span></span> <span data-ttu-id="b6227-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em RolePoint precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="b6227-140">In other words, a link relationship between an Azure AD user and hello related user in RolePoint needs toobe established.</span></span>

<span data-ttu-id="b6227-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em RolePoint.</span><span class="sxs-lookup"><span data-stu-id="b6227-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in RolePoint.</span></span>

<span data-ttu-id="b6227-142">tooconfigure e teste de logon único do AD do Azure com RolePoint, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="b6227-142">tooconfigure and test Azure AD single sign-on with RolePoint, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b6227-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="b6227-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b6227-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6227-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b6227-145">**[Criar um usuário de teste RolePoint](#creating-a-rolepoint-test-user)**  -toohave um equivalente do Britta Simon em RolePoint é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="b6227-145">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - toohave a counterpart of Britta Simon in RolePoint that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b6227-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="b6227-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b6227-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="b6227-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b6227-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6227-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b6227-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo RolePoint.</span><span class="sxs-lookup"><span data-stu-id="b6227-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RolePoint application.</span></span>

<span data-ttu-id="b6227-150">**tooconfigure AD do Azure-logon único com RolePoint, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b6227-150">**tooconfigure Azure AD single sign-on with RolePoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="b6227-151">Em Olá portal do Azure, Olá **RolePoint** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="b6227-151">In hello Azure portal, on hello **RolePoint** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="b6227-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="b6227-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_samlbase.png)

3. <span data-ttu-id="b6227-155">Em Olá **RolePoint domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b6227-155">On hello **RolePoint Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_url.png)

    <span data-ttu-id="b6227-157">a.</span><span class="sxs-lookup"><span data-stu-id="b6227-157">a.</span></span> <span data-ttu-id="b6227-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.rolepoint.com/login`</span><span class="sxs-lookup"><span data-stu-id="b6227-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.rolepoint.com/login`</span></span>
    
    <span data-ttu-id="b6227-159">b.</span><span class="sxs-lookup"><span data-stu-id="b6227-159">b.</span></span> <span data-ttu-id="b6227-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://app.rolepoint.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="b6227-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://app.rolepoint.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b6227-161">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="b6227-161">These values are not hello real.</span></span> <span data-ttu-id="b6227-162">Atualize esses valores com URL de logon real hello e o identificador.</span><span class="sxs-lookup"><span data-stu-id="b6227-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="b6227-163">Aqui nós sugerimos você toouse valor exclusivo do hello da cadeia de caracteres hello Identifier.Contact [RolePoint a equipe de suporte](mailto:info@rolepoint.com) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6227-163">Here we suggest you toouse hello unique value of string in hello Identifier.Contact [RolePoint support team](mailto:info@rolepoint.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="b6227-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="b6227-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_certificate.png) 

5. <span data-ttu-id="b6227-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="b6227-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rolepoint-tutorial/tutorial_general_400.png)


6. <span data-ttu-id="b6227-168">tooconfigure logon único no **RolePoint** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte RolePoint](mailto:info@rolepoint.com).</span><span class="sxs-lookup"><span data-stu-id="b6227-168">tooconfigure single sign-on on **RolePoint** side, you need toosend hello downloaded **Metadata XML** too[RolePoint support team](mailto:info@rolepoint.com).</span></span>

> [!TIP]
> <span data-ttu-id="b6227-169">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="b6227-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b6227-170">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="b6227-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b6227-171">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b6227-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b6227-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b6227-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="b6227-173">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6227-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="b6227-175">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b6227-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b6227-176">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="b6227-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b6227-178">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="b6227-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b6227-180">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6227-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b6227-182">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b6227-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b6227-184">a.</span><span class="sxs-lookup"><span data-stu-id="b6227-184">a.</span></span> <span data-ttu-id="b6227-185">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b6227-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b6227-186">b.</span><span class="sxs-lookup"><span data-stu-id="b6227-186">b.</span></span> <span data-ttu-id="b6227-187">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b6227-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b6227-188">c.</span><span class="sxs-lookup"><span data-stu-id="b6227-188">c.</span></span> <span data-ttu-id="b6227-189">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="b6227-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b6227-190">d.</span><span class="sxs-lookup"><span data-stu-id="b6227-190">d.</span></span> <span data-ttu-id="b6227-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b6227-191">Click **Create**.</span></span>
 
### <a name="creating-a-rolepoint-test-user"></a><span data-ttu-id="b6227-192">Criando um usuário de teste do RolePoint</span><span class="sxs-lookup"><span data-stu-id="b6227-192">Creating a RolePoint test user</span></span>

<span data-ttu-id="b6227-193">Nesta seção, você criará um usuário chamado Brenda Fernandes no RolePoint.</span><span class="sxs-lookup"><span data-stu-id="b6227-193">In this section, you create a user called Britta Simon in RolePoint.</span></span> <span data-ttu-id="b6227-194">Trabalhar com [RolePoint a equipe de suporte](mailto:info@rolepoint.com) tooadd usuários de saudação na plataforma de RolePoint hello.</span><span class="sxs-lookup"><span data-stu-id="b6227-194">Work with [RolePoint support team](mailto:info@rolepoint.com) tooadd hello users in hello RolePoint platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b6227-195">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="b6227-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b6227-196">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooRolePoint.</span><span class="sxs-lookup"><span data-stu-id="b6227-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRolePoint.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="b6227-198">**tooassign Britta Simon tooRolePoint, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="b6227-198">**tooassign Britta Simon tooRolePoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="b6227-199">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="b6227-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="b6227-201">Na lista de aplicativos hello, selecione **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="b6227-201">In hello applications list, select **RolePoint**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_app.png) 

3. <span data-ttu-id="b6227-203">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="b6227-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="b6227-205">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="b6227-205">Click **Add** button.</span></span> <span data-ttu-id="b6227-206">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b6227-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="b6227-208">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6227-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b6227-209">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b6227-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b6227-210">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="b6227-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b6227-211">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="b6227-211">Testing single sign-on</span></span>

<span data-ttu-id="b6227-212">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="b6227-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b6227-213">Quando você clica em bloco RolePoint Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour RolePoint aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6227-213">When you click hello RolePoint tile in hello Access Panel, you should get automatically signed-on tooyour RolePoint application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b6227-214">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="b6227-214">Additional resources</span></span>

* [<span data-ttu-id="b6227-215">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="b6227-215">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b6227-216">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b6227-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_203.png

