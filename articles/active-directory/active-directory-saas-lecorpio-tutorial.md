---
title: "Tutorial: integração do Azure Active Directory ao Lecorpio | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Lecorpio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 963eb36678c589f942f63c7ab555161255324717
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lecorpio"></a><span data-ttu-id="10852-103">Tutorial: integração do Azure Active Directory com o Lecorpio</span><span class="sxs-lookup"><span data-stu-id="10852-103">Tutorial: Azure Active Directory integration with Lecorpio</span></span>

<span data-ttu-id="10852-104">Neste tutorial, você aprenderá como toointegrate Lecorpio com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="10852-104">In this tutorial, you learn how toointegrate Lecorpio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="10852-105">Integrando Lecorpio com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="10852-105">Integrating Lecorpio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="10852-106">Você pode controlar no AD do Azure que tenha acesso tooLecorpio</span><span class="sxs-lookup"><span data-stu-id="10852-106">You can control in Azure AD who has access tooLecorpio</span></span>
- <span data-ttu-id="10852-107">Você pode habilitar seu usuários tooautomatically get conectado tooLecorpio (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10852-107">You can enable your users tooautomatically get signed-on tooLecorpio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="10852-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="10852-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="10852-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="10852-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10852-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="10852-110">Prerequisites</span></span>

<span data-ttu-id="10852-111">tooconfigure integração do AD do Azure com Lecorpio, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="10852-111">tooconfigure Azure AD integration with Lecorpio, you need hello following items:</span></span>

- <span data-ttu-id="10852-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10852-112">An Azure AD subscription</span></span>
- <span data-ttu-id="10852-113">Uma assinatura habilitada para logon único do Lecorpio</span><span class="sxs-lookup"><span data-stu-id="10852-113">A Lecorpio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="10852-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="10852-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="10852-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="10852-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="10852-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="10852-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="10852-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="10852-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="10852-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="10852-118">Scenario description</span></span>
<span data-ttu-id="10852-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="10852-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="10852-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="10852-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="10852-121">Adicionando Lecorpio da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="10852-121">Adding Lecorpio from hello gallery</span></span>
2. <span data-ttu-id="10852-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10852-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lecorpio-from-hello-gallery"></a><span data-ttu-id="10852-123">Adicionando Lecorpio da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="10852-123">Adding Lecorpio from hello gallery</span></span>
<span data-ttu-id="10852-124">integração de saudação tooconfigure de Lecorpio no AD do Azure, você precisa tooadd Lecorpio da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="10852-124">tooconfigure hello integration of Lecorpio into Azure AD, you need tooadd Lecorpio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="10852-125">**tooadd Lecorpio da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="10852-125">**tooadd Lecorpio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="10852-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="10852-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="10852-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="10852-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="10852-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="10852-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="10852-131">Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="10852-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="10852-133">Na caixa de pesquisa hello, digite **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="10852-133">In hello search box, type **Lecorpio**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_search.png)

5. <span data-ttu-id="10852-135">No painel de resultados de saudação, selecione **Lecorpio**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="10852-135">In hello results panel, select **Lecorpio**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="10852-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10852-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="10852-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Lecorpio, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="10852-138">In this section, you configure and test Azure AD single sign-on with Lecorpio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="10852-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Lecorpio é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="10852-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lecorpio is tooa user in Azure AD.</span></span> <span data-ttu-id="10852-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Lecorpio precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="10852-140">In other words, a link relationship between an Azure AD user and hello related user in Lecorpio needs toobe established.</span></span>

<span data-ttu-id="10852-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **nome de usuário** em Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="10852-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lecorpio.</span></span>

<span data-ttu-id="10852-142">tooconfigure e teste de logon único do AD do Azure com Lecorpio, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="10852-142">tooconfigure and test Azure AD single sign-on with Lecorpio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="10852-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="10852-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="10852-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="10852-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="10852-145">**[Criar um usuário de teste Lecorpio](#creating-a-lecorpio-test-user)**  -toohave um equivalente do Britta Simon em Lecorpio é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="10852-145">**[Creating a Lecorpio test user](#creating-a-lecorpio-test-user)** - toohave a counterpart of Britta Simon in Lecorpio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="10852-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="10852-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="10852-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="10852-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="10852-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="10852-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="10852-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="10852-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lecorpio application.</span></span>

<span data-ttu-id="10852-150">**tooconfigure AD do Azure-logon único com Lecorpio, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="10852-150">**tooconfigure Azure AD single sign-on with Lecorpio, perform hello following steps:**</span></span>

1. <span data-ttu-id="10852-151">Em Olá portal do Azure, Olá **Lecorpio** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="10852-151">In hello Azure portal, on hello **Lecorpio** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="10852-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="10852-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_samlbase.png)

3. <span data-ttu-id="10852-155">Em Olá **Lecorpio domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="10852-155">On hello **Lecorpio Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_url.png)

    <span data-ttu-id="10852-157">a.</span><span class="sxs-lookup"><span data-stu-id="10852-157">a.</span></span> <span data-ttu-id="10852-158">Em Olá **URL de logon** texto, o valor do tipo hello usando saudação padrão a seguir:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="10852-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    <span data-ttu-id="10852-159">b.</span><span class="sxs-lookup"><span data-stu-id="10852-159">b.</span></span> <span data-ttu-id="10852-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<instance name>.lecorpio.com/<customer name>`</span><span class="sxs-lookup"><span data-stu-id="10852-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instance name>.lecorpio.com/<customer name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="10852-161">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="10852-161">These values are not hello real.</span></span> <span data-ttu-id="10852-162">Atualize esses valores com URL de logon real hello e o identificador.</span><span class="sxs-lookup"><span data-stu-id="10852-162">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="10852-163">Aqui, é recomendável você toouse Olá valor exclusivo de cadeia de caracteres em identificador de saudação.</span><span class="sxs-lookup"><span data-stu-id="10852-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="10852-164">Entre em contato com [equipe de suporte do cliente Lecorpio](mailto:info@lecorpio.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="10852-164">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="10852-165">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="10852-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_certificate.png) 

5. <span data-ttu-id="10852-167">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="10852-167">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lecorpio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="10852-169">tooconfigure logon único no **Lecorpio** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte Lecorpio](mailto:info@lecorpio.com).</span><span class="sxs-lookup"><span data-stu-id="10852-169">tooconfigure single sign-on on **Lecorpio** side, you need toosend hello downloaded **Metadata XML** too[Lecorpio support team](mailto:info@lecorpio.com).</span></span>

> [!TIP]
> <span data-ttu-id="10852-170">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="10852-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="10852-171">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="10852-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="10852-172">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="10852-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="10852-173">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10852-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="10852-174">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="10852-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="10852-176">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="10852-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="10852-177">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="10852-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="10852-179">Vá muito**usuários e grupos** e clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="10852-179">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="10852-181">Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="10852-181">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="10852-183">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="10852-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-lecorpio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="10852-185">a.</span><span class="sxs-lookup"><span data-stu-id="10852-185">a.</span></span> <span data-ttu-id="10852-186">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="10852-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="10852-187">b.</span><span class="sxs-lookup"><span data-stu-id="10852-187">b.</span></span> <span data-ttu-id="10852-188">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="10852-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="10852-189">c.</span><span class="sxs-lookup"><span data-stu-id="10852-189">c.</span></span> <span data-ttu-id="10852-190">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="10852-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="10852-191">d.</span><span class="sxs-lookup"><span data-stu-id="10852-191">d.</span></span> <span data-ttu-id="10852-192">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="10852-192">Click **Create**.</span></span>
 
### <a name="creating-a-lecorpio-test-user"></a><span data-ttu-id="10852-193">Criando um usuário de teste do Lecorpio</span><span class="sxs-lookup"><span data-stu-id="10852-193">Creating a Lecorpio test user</span></span>

<span data-ttu-id="10852-194">Nesta seção, você criará um usuário chamado Brenda Fernandes no Lecorpio.</span><span class="sxs-lookup"><span data-stu-id="10852-194">In this section, you create a user called Britta Simon in Lecorpio.</span></span> 

<span data-ttu-id="10852-195">Entre em contato com [equipe de suporte do cliente Lecorpio](mailto:info@lecorpio.com) tooadd usuários Olá Olá Lecorpio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="10852-195">Contact [Lecorpio Client support team](mailto:info@lecorpio.com) tooadd hello users in hello Lecorpio application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="10852-196">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10852-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="10852-197">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLecorpio.</span><span class="sxs-lookup"><span data-stu-id="10852-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLecorpio.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="10852-199">**tooassign Britta Simon tooLecorpio, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="10852-199">**tooassign Britta Simon tooLecorpio, perform hello following steps:**</span></span>

1. <span data-ttu-id="10852-200">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="10852-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="10852-202">Na lista de aplicativos hello, selecione **Lecorpio**.</span><span class="sxs-lookup"><span data-stu-id="10852-202">In hello applications list, select **Lecorpio**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-lecorpio-tutorial/tutorial_lecorpio_app.png) 

3. <span data-ttu-id="10852-204">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="10852-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="10852-206">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="10852-206">Click **Add** button.</span></span> <span data-ttu-id="10852-207">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="10852-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="10852-209">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="10852-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="10852-210">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="10852-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="10852-211">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="10852-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="10852-212">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="10852-212">Testing single sign-on</span></span>

<span data-ttu-id="10852-213">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="10852-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="10852-214">Quando você clica em bloco Lecorpio Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Lecorpio aplicativo.</span><span class="sxs-lookup"><span data-stu-id="10852-214">When you click hello Lecorpio tile in hello Access Panel, you should get automatically signed-on tooyour Lecorpio application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="10852-215">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="10852-215">Additional resources</span></span>

* [<span data-ttu-id="10852-216">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="10852-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="10852-217">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="10852-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lecorpio-tutorial/tutorial_general_203.png

