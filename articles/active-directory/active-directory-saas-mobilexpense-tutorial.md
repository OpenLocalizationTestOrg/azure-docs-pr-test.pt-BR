---
title: "Tutorial: Integração do Azure Active Directory com o MobileXpense | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e MobileXpense."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e649fc4e-3e15-4948-b977-00bfe9f7db13
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: jeedes
ms.openlocfilehash: b9d109f9d4244f8a7eb8b49b0d980cd3df0fc59d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mobilexpense"></a><span data-ttu-id="17f37-103">Tutorial: integração do Azure Active Directory ao MobileXpense</span><span class="sxs-lookup"><span data-stu-id="17f37-103">Tutorial: Azure Active Directory integration with MobileXpense</span></span>

<span data-ttu-id="17f37-104">Neste tutorial, você aprenderá como toointegrate MobileXpense com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="17f37-104">In this tutorial, you learn how toointegrate MobileXpense with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17f37-105">Integrando MobileXpense com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="17f37-105">Integrating MobileXpense with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="17f37-106">Você pode controlar no AD do Azure que tenha acesso tooMobileXpense</span><span class="sxs-lookup"><span data-stu-id="17f37-106">You can control in Azure AD who has access tooMobileXpense</span></span>
- <span data-ttu-id="17f37-107">Você pode habilitar seu usuários tooautomatically get conectado tooMobileXpense (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="17f37-107">You can enable your users tooautomatically get signed-on tooMobileXpense (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17f37-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="17f37-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="17f37-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17f37-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17f37-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="17f37-110">Prerequisites</span></span>

<span data-ttu-id="17f37-111">tooconfigure integração do AD do Azure com MobileXpense, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="17f37-111">tooconfigure Azure AD integration with MobileXpense, you need hello following items:</span></span>

- <span data-ttu-id="17f37-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="17f37-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17f37-113">Uma assinatura do MobileXpense habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="17f37-113">A MobileXpense single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17f37-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="17f37-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17f37-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="17f37-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17f37-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="17f37-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17f37-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17f37-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17f37-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="17f37-118">Scenario description</span></span>
<span data-ttu-id="17f37-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="17f37-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17f37-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="17f37-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17f37-121">Adicionando MobileXpense da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="17f37-121">Adding MobileXpense from hello gallery</span></span>
2. <span data-ttu-id="17f37-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="17f37-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mobilexpense-from-hello-gallery"></a><span data-ttu-id="17f37-123">Adicionando MobileXpense da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="17f37-123">Adding MobileXpense from hello gallery</span></span>
<span data-ttu-id="17f37-124">integração de saudação tooconfigure de MobileXpense no AD do Azure, você precisa tooadd MobileXpense da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="17f37-124">tooconfigure hello integration of MobileXpense into Azure AD, you need tooadd MobileXpense from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="17f37-125">**tooadd MobileXpense da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="17f37-125">**tooadd MobileXpense from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="17f37-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="17f37-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="17f37-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="17f37-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="17f37-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="17f37-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="17f37-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17f37-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="17f37-133">Na caixa de pesquisa hello, digite **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="17f37-133">In hello search box, type **MobileXpense**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_search.png)

5. <span data-ttu-id="17f37-135">No painel de resultados de saudação, selecione **MobileXpense**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="17f37-135">In hello results panel, select **MobileXpense**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17f37-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="17f37-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17f37-138">Nesta seção, você configurará e testará o logon único do Azure AD com o MobileXpense, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="17f37-138">In this section, you configure and test Azure AD single sign-on with MobileXpense based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="17f37-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em MobileXpense é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="17f37-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MobileXpense is tooa user in Azure AD.</span></span> <span data-ttu-id="17f37-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em MobileXpense precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="17f37-140">In other words, a link relationship between an Azure AD user and hello related user in MobileXpense needs toobe established.</span></span>

<span data-ttu-id="17f37-141">MobileXpense, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="17f37-141">In MobileXpense, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="17f37-142">tooconfigure e teste de logon único do AD do Azure com MobileXpense, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="17f37-142">tooconfigure and test Azure AD single sign-on with MobileXpense, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="17f37-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="17f37-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="17f37-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17f37-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17f37-145">**[Criar um usuário de teste MobileXpense](#creating-a-mobilexpense-test-user)**  -toohave um equivalente do Britta Simon em MobileXpense é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="17f37-145">**[Creating a MobileXpense test user](#creating-a-mobilexpense-test-user)** - toohave a counterpart of Britta Simon in MobileXpense that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="17f37-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="17f37-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17f37-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="17f37-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17f37-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="17f37-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17f37-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="17f37-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MobileXpense application.</span></span>

<span data-ttu-id="17f37-150">**tooconfigure AD do Azure-logon único com MobileXpense, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="17f37-150">**tooconfigure Azure AD single sign-on with MobileXpense, perform hello following steps:**</span></span>

1. <span data-ttu-id="17f37-151">Em Olá portal do Azure, Olá **MobileXpense** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="17f37-151">In hello Azure portal, on hello **MobileXpense** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="17f37-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="17f37-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_samlbase.png)

3. <span data-ttu-id="17f37-155">Em Olá **MobileXpense domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="17f37-155">On hello **MobileXpense Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url11.png)

    <span data-ttu-id="17f37-157">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="17f37-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span></span>

4. <span data-ttu-id="17f37-158">Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="17f37-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url22.png)

<span data-ttu-id="17f37-160">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<sub domain>.mobilexpense.com/<customername>`</span><span class="sxs-lookup"><span data-stu-id="17f37-160">In hello **Sign-on URL** textbox, type a URL using hello following pattern:: `https://<sub domain>.mobilexpense.com/<customername>`</span></span>

> [!NOTE] 
> <span data-ttu-id="17f37-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="17f37-161">These values are not real.</span></span> <span data-ttu-id="17f37-162">Atualize esses valores com URL de resposta real hello e a URL de logon.</span><span class="sxs-lookup"><span data-stu-id="17f37-162">Update these values with hello actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="17f37-163">Entre em contato com [equipe de suporte do cliente MobileXpense](http://www.mobilexpense.net/contact) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="17f37-163">Contact [MobileXpense Client support team](http://www.mobilexpense.net/contact) tooget these values.</span></span> 

5. <span data-ttu-id="17f37-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="17f37-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_certificate.png) 

6. <span data-ttu-id="17f37-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="17f37-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="17f37-168">tooconfigure logon único no **MobileXpense** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte MobileXpense](http://www.mobilexpense.net/contact).</span><span class="sxs-lookup"><span data-stu-id="17f37-168">tooconfigure single sign-on on **MobileXpense** side, you need toosend hello downloaded **Metadata XML** too[MobileXpense support team](http://www.mobilexpense.net/contact).</span></span>

> [!TIP]
> <span data-ttu-id="17f37-169">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="17f37-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="17f37-170">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="17f37-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="17f37-171">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17f37-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17f37-172">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="17f37-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="17f37-173">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="17f37-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="17f37-175">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="17f37-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="17f37-176">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="17f37-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17f37-178">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="17f37-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17f37-180">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="17f37-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17f37-182">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="17f37-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17f37-184">a.</span><span class="sxs-lookup"><span data-stu-id="17f37-184">a.</span></span> <span data-ttu-id="17f37-185">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17f37-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17f37-186">b.</span><span class="sxs-lookup"><span data-stu-id="17f37-186">b.</span></span> <span data-ttu-id="17f37-187">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="17f37-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17f37-188">c.</span><span class="sxs-lookup"><span data-stu-id="17f37-188">c.</span></span> <span data-ttu-id="17f37-189">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="17f37-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="17f37-190">d.</span><span class="sxs-lookup"><span data-stu-id="17f37-190">d.</span></span> <span data-ttu-id="17f37-191">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="17f37-191">Click **Create**.</span></span>
 
### <a name="creating-a-mobilexpense-test-user"></a><span data-ttu-id="17f37-192">Criar um usuário de teste do MobileXpense</span><span class="sxs-lookup"><span data-stu-id="17f37-192">Creating a MobileXpense test user</span></span>

<span data-ttu-id="17f37-193">Nesta seção, você criará uma usuária chamada Brenda Fernandes no MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="17f37-193">In this section, you create a user called Britta Simon in MobileXpense.</span></span> <span data-ttu-id="17f37-194">trabalhar com [MobileXpense a equipe de suporte](http://www.mobilexpense.net/contact) para adicionar usuários de saudação na plataforma de MobileXpense hello.</span><span class="sxs-lookup"><span data-stu-id="17f37-194">work with [MobileXpense support team](http://www.mobilexpense.net/contact) to add hello users in hello MobileXpense platform.</span></span> <span data-ttu-id="17f37-195">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="17f37-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="17f37-196">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="17f37-196">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="17f37-197">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooMobileXpense.</span><span class="sxs-lookup"><span data-stu-id="17f37-197">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMobileXpense.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="17f37-199">**tooassign Britta Simon tooMobileXpense, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="17f37-199">**tooassign Britta Simon tooMobileXpense, perform hello following steps:**</span></span>

1. <span data-ttu-id="17f37-200">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="17f37-200">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="17f37-202">Na lista de aplicativos hello, selecione **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="17f37-202">In hello applications list, select **MobileXpense**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_app.png) 

3. <span data-ttu-id="17f37-204">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="17f37-204">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="17f37-206">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="17f37-206">Click **Add** button.</span></span> <span data-ttu-id="17f37-207">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17f37-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="17f37-209">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="17f37-209">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="17f37-210">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17f37-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17f37-211">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="17f37-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17f37-212">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="17f37-212">Testing single sign-on</span></span>

<span data-ttu-id="17f37-213">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="17f37-213">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="17f37-214">Quando você clica em bloco MobileXpense Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour MobileXpense aplicativo.</span><span class="sxs-lookup"><span data-stu-id="17f37-214">When you click hello MobileXpense tile in hello Access Panel, you should get automatically signed-on tooyour MobileXpense application.</span></span>
<span data-ttu-id="17f37-215">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="17f37-215">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="17f37-216">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="17f37-216">Additional resources</span></span>

* [<span data-ttu-id="17f37-217">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="17f37-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17f37-218">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="17f37-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_203.png

