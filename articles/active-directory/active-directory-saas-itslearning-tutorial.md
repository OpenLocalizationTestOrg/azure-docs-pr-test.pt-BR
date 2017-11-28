---
title: "Tutorial: Integração do Azure Active Directory ao itslearning | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e itslearning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 60587ba3-1396-4b8a-9ac1-e22a98e5e0ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 4ee6c8d450cc3972a87da67fc79890473cfa498a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itslearning"></a><span data-ttu-id="24bb1-103">Tutorial: Integração do Azure Active Directory ao itslearning</span><span class="sxs-lookup"><span data-stu-id="24bb1-103">Tutorial: Azure Active Directory integration with itslearning</span></span>

<span data-ttu-id="24bb1-104">Neste tutorial, você aprenderá como itslearning toointegrate com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="24bb1-104">In this tutorial, you learn how toointegrate itslearning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24bb1-105">Integrando itslearning com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="24bb1-105">Integrating itslearning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="24bb1-106">Você pode controlar no AD do Azure que tenha acesso tooitslearning</span><span class="sxs-lookup"><span data-stu-id="24bb1-106">You can control in Azure AD who has access tooitslearning</span></span>
- <span data-ttu-id="24bb1-107">Você pode habilitar seu usuários tooautomatically get conectado tooitslearning (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="24bb1-107">You can enable your users tooautomatically get signed-on tooitslearning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="24bb1-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="24bb1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="24bb1-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="24bb1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24bb1-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="24bb1-110">Prerequisites</span></span>

<span data-ttu-id="24bb1-111">tooconfigure integração do AD do Azure com itslearning, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="24bb1-111">tooconfigure Azure AD integration with itslearning, you need hello following items:</span></span>

- <span data-ttu-id="24bb1-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="24bb1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24bb1-113">Uma assinatura habilitada para logon único do itslearning</span><span class="sxs-lookup"><span data-stu-id="24bb1-113">An itslearning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24bb1-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="24bb1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24bb1-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="24bb1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24bb1-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="24bb1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24bb1-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24bb1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24bb1-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="24bb1-118">Scenario description</span></span>
<span data-ttu-id="24bb1-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="24bb1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24bb1-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="24bb1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24bb1-121">Adicionando itslearning da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="24bb1-121">Adding itslearning from hello gallery</span></span>
2. <span data-ttu-id="24bb1-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="24bb1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itslearning-from-hello-gallery"></a><span data-ttu-id="24bb1-123">Adicionando itslearning da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="24bb1-123">Adding itslearning from hello gallery</span></span>
<span data-ttu-id="24bb1-124">integração de saudação tooconfigure de itslearning no AD do Azure, você precisa itslearning tooadd da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="24bb1-124">tooconfigure hello integration of itslearning into Azure AD, you need tooadd itslearning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="24bb1-125">**itslearning tooadd da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="24bb1-125">**tooadd itslearning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="24bb1-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="24bb1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="24bb1-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="24bb1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="24bb1-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="24bb1-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="24bb1-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24bb1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="24bb1-133">Na caixa de pesquisa hello, digite **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="24bb1-133">In hello search box, type **itslearning**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_search.png)

5. <span data-ttu-id="24bb1-135">No painel de resultados de saudação, selecione **itslearning**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="24bb1-135">In hello results panel, select **itslearning**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="24bb1-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="24bb1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="24bb1-138">Nesta seção, você configura e testa o logon único do Azure AD com o itslearning com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="24bb1-138">In this section, you configure and test Azure AD single sign-on with itslearning based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="24bb1-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em itslearning é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="24bb1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in itslearning is tooa user in Azure AD.</span></span> <span data-ttu-id="24bb1-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em itslearning precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="24bb1-140">In other words, a link relationship between an Azure AD user and hello related user in itslearning needs toobe established.</span></span>

<span data-ttu-id="24bb1-141">Itslearning, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="24bb1-141">In itslearning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="24bb1-142">tooconfigure e teste de logon único do AD do Azure com itslearning, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="24bb1-142">tooconfigure and test Azure AD single sign-on with itslearning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="24bb1-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="24bb1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="24bb1-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="24bb1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24bb1-145">**[Criar um usuário de teste itslearning](#creating-an-itslearning-test-user)**  -toohave um equivalente do Britta Simon em itslearning é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="24bb1-145">**[Creating an itslearning test user](#creating-an-itslearning-test-user)** - toohave a counterpart of Britta Simon in itslearning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="24bb1-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="24bb1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24bb1-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="24bb1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="24bb1-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="24bb1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="24bb1-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo itslearning.</span><span class="sxs-lookup"><span data-stu-id="24bb1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your itslearning application.</span></span>

<span data-ttu-id="24bb1-150">**tooconfigure AD do Azure-logon único com itslearning, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="24bb1-150">**tooconfigure Azure AD single sign-on with itslearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="24bb1-151">Em Olá portal do Azure, Olá **itslearning** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="24bb1-151">In hello Azure portal, on hello **itslearning** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="24bb1-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="24bb1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_samlbase.png)

3. <span data-ttu-id="24bb1-155">Em Olá **itslearning domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="24bb1-155">On hello **itslearning Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_url.png)

    <span data-ttu-id="24bb1-157">a.</span><span class="sxs-lookup"><span data-stu-id="24bb1-157">a.</span></span> <span data-ttu-id="24bb1-158">Em Olá **URL de logon** caixa de texto, digite um URL como:</span><span class="sxs-lookup"><span data-stu-id="24bb1-158">In hello **Sign-on URL** textbox, type a URL as:</span></span>
    | |
    |--| 
    | `https://www.itslearning.com/index.aspx`|
    | `https://us1.itslearning.com/index.aspx`|

    <span data-ttu-id="24bb1-159">b.</span><span class="sxs-lookup"><span data-stu-id="24bb1-159">b.</span></span> <span data-ttu-id="24bb1-160">Em Olá **identificador** caixa de texto, digite um URL como:`urn:mace:saml2v2.no:services:com.itslearning`</span><span class="sxs-lookup"><span data-stu-id="24bb1-160">In hello **Identifier** textbox, type a URL as: `urn:mace:saml2v2.no:services:com.itslearning`</span></span>

4. <span data-ttu-id="24bb1-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="24bb1-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_certificate.png) 

5. <span data-ttu-id="24bb1-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="24bb1-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-itslearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="24bb1-165">tooconfigure logon único no **itslearning** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte itslearning](mailto:support@itslearning.com).</span><span class="sxs-lookup"><span data-stu-id="24bb1-165">tooconfigure single sign-on on **itslearning** side, you need toosend hello downloaded **Metadata XML** too[itslearning support team](mailto:support@itslearning.com).</span></span> <span data-ttu-id="24bb1-166">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="24bb1-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="24bb1-167">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="24bb1-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="24bb1-168">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="24bb1-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="24bb1-169">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24bb1-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="24bb1-170">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="24bb1-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="24bb1-171">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="24bb1-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="24bb1-173">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="24bb1-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="24bb1-174">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="24bb1-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itslearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="24bb1-176">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="24bb1-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itslearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="24bb1-178">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="24bb1-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itslearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="24bb1-180">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="24bb1-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-itslearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="24bb1-182">a.</span><span class="sxs-lookup"><span data-stu-id="24bb1-182">a.</span></span> <span data-ttu-id="24bb1-183">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="24bb1-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24bb1-184">b.</span><span class="sxs-lookup"><span data-stu-id="24bb1-184">b.</span></span> <span data-ttu-id="24bb1-185">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="24bb1-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="24bb1-186">c.</span><span class="sxs-lookup"><span data-stu-id="24bb1-186">c.</span></span> <span data-ttu-id="24bb1-187">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="24bb1-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="24bb1-188">d.</span><span class="sxs-lookup"><span data-stu-id="24bb1-188">d.</span></span> <span data-ttu-id="24bb1-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="24bb1-189">Click **Create**.</span></span>
 
### <a name="creating-an-itslearning-test-user"></a><span data-ttu-id="24bb1-190">Como criar um usuário de teste do itslearning</span><span class="sxs-lookup"><span data-stu-id="24bb1-190">Creating an itslearning test user</span></span>

<span data-ttu-id="24bb1-191">Nesta seção, você cria um usuário chamado Brenda Fernandes no itslearning.</span><span class="sxs-lookup"><span data-stu-id="24bb1-191">In this section, you create a user called Britta Simon in itslearning.</span></span> <span data-ttu-id="24bb1-192">Trabalhar com [a equipe de suporte de cliente itslearning](mailto:support@itslearning.com) para adicionar usuários de saudação na plataforma de itslearning hello.</span><span class="sxs-lookup"><span data-stu-id="24bb1-192">Work with [itslearning Client support team](mailto:support@itslearning.com) to add hello users in hello itslearning platform.</span></span> <span data-ttu-id="24bb1-193">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="24bb1-193">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="24bb1-194">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="24bb1-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="24bb1-195">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooitslearning.</span><span class="sxs-lookup"><span data-stu-id="24bb1-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooitslearning.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="24bb1-197">**tooassign Britta Simon tooitslearning, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="24bb1-197">**tooassign Britta Simon tooitslearning, perform hello following steps:**</span></span>

1. <span data-ttu-id="24bb1-198">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="24bb1-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="24bb1-200">Na lista de aplicativos hello, selecione **itslearning**.</span><span class="sxs-lookup"><span data-stu-id="24bb1-200">In hello applications list, select **itslearning**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-itslearning-tutorial/tutorial_itslearning_app.png) 

3. <span data-ttu-id="24bb1-202">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="24bb1-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="24bb1-204">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="24bb1-204">Click **Add** button.</span></span> <span data-ttu-id="24bb1-205">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24bb1-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="24bb1-207">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="24bb1-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="24bb1-208">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24bb1-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24bb1-209">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="24bb1-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="24bb1-210">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="24bb1-210">Testing single sign-on</span></span>

<span data-ttu-id="24bb1-211">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="24bb1-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="24bb1-212">Quando você clica em bloco itslearning Olá Olá painel de acesso, você deve obter a página de logon do aplicativo itslearning.</span><span class="sxs-lookup"><span data-stu-id="24bb1-212">When you click hello itslearning tile in hello Access Panel, you should get login page of itslearning application.</span></span> <span data-ttu-id="24bb1-213">Clique em **fazer logon com o Windows Azure ACS1** para logon com êxito no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="24bb1-213">Click **Log in with Windows Azure ACS1** for successful login into hello application.</span></span>

  ![Logon](./media/active-directory-saas-itslearning-tutorial/login.png)

<span data-ttu-id="24bb1-215">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="24bb1-215">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24bb1-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="24bb1-216">Additional resources</span></span>

* [<span data-ttu-id="24bb1-217">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="24bb1-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24bb1-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="24bb1-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itslearning-tutorial/tutorial_general_203.png

