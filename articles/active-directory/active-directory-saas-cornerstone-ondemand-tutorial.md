---
title: "Tutorial: integração do Azure Active Directory com o Cornerstone OnDemand | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Cornerstone OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f57c5fef-49b0-4591-91ef-fc0de6d654ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 85fd6eb4e93010d8f7477df236403e205e9f2d83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cornerstone-ondemand"></a><span data-ttu-id="eb036-103">Tutorial: integração do Active Directory do Azure ao Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="eb036-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span></span>

<span data-ttu-id="eb036-104">Neste tutorial, você aprenderá como toointegrate Cornerstone OnDemand com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="eb036-104">In this tutorial, you learn how toointegrate Cornerstone OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eb036-105">Integrando o Cornerstone OnDemand com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="eb036-105">Integrating Cornerstone OnDemand with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="eb036-106">Você pode controlar no AD do Azure que tenha acesso tooCornerstone sob demanda</span><span class="sxs-lookup"><span data-stu-id="eb036-106">You can control in Azure AD who has access tooCornerstone OnDemand</span></span>
- <span data-ttu-id="eb036-107">Você pode habilitar seu usuários tooautomatically get conectado tooCornerstone OnDemand (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eb036-107">You can enable your users tooautomatically get signed-on tooCornerstone OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="eb036-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="eb036-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="eb036-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eb036-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb036-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="eb036-110">Prerequisites</span></span>

<span data-ttu-id="eb036-111">tooconfigure integração do AD do Azure com o Cornerstone OnDemand, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="eb036-111">tooconfigure Azure AD integration with Cornerstone OnDemand, you need hello following items:</span></span>

- <span data-ttu-id="eb036-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eb036-112">An Azure AD subscription</span></span>
- <span data-ttu-id="eb036-113">Uma assinatura habilitada para logon único do Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="eb036-113">A Cornerstone OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="eb036-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="eb036-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="eb036-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="eb036-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="eb036-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="eb036-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="eb036-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eb036-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eb036-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="eb036-118">Scenario description</span></span>
<span data-ttu-id="eb036-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="eb036-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="eb036-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="eb036-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eb036-121">Adicionando Cornerstone OnDemand da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="eb036-121">Adding Cornerstone OnDemand from hello gallery</span></span>
2. <span data-ttu-id="eb036-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eb036-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cornerstone-ondemand-from-hello-gallery"></a><span data-ttu-id="eb036-123">Adicionando Cornerstone OnDemand da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="eb036-123">Adding Cornerstone OnDemand from hello gallery</span></span>
<span data-ttu-id="eb036-124">integração de saudação tooconfigure do Cornerstone OnDemand no AD do Azure, você precisa tooadd Cornerstone OnDemand na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="eb036-124">tooconfigure hello integration of Cornerstone OnDemand into Azure AD, you need tooadd Cornerstone OnDemand from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="eb036-125">**tooadd Cornerstone OnDemand da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eb036-125">**tooadd Cornerstone OnDemand from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb036-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="eb036-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="eb036-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="eb036-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="eb036-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="eb036-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="eb036-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eb036-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="eb036-133">Na caixa de pesquisa hello, digite **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="eb036-133">In hello search box, type **Cornerstone OnDemand**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_search.png)

5. <span data-ttu-id="eb036-135">No painel de resultados de saudação, selecione **Cornerstone OnDemand**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="eb036-135">In hello results panel, select **Cornerstone OnDemand**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eb036-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eb036-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eb036-138">Nesta seção, você configura e testa o logon único do Azure AD com o Cornerstone OnDemand com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="eb036-138">In this section, you configure and test Azure AD single sign-on with Cornerstone OnDemand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="eb036-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Cornerstone OnDemand é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb036-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cornerstone OnDemand is tooa user in Azure AD.</span></span> <span data-ttu-id="eb036-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Cornerstone OnDemand precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="eb036-140">In other words, a link relationship between an Azure AD user and hello related user in Cornerstone OnDemand needs toobe established.</span></span>

<span data-ttu-id="eb036-141">No Cornerstone OnDemand, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb036-141">In Cornerstone OnDemand, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="eb036-142">tooconfigure e teste de logon único do AD do Azure com o Cornerstone OnDemand, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="eb036-142">tooconfigure and test Azure AD single sign-on with Cornerstone OnDemand, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="eb036-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="eb036-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="eb036-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="eb036-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eb036-145">**[Criar um usuário de teste do Cornerstone OnDemand](#creating-a-cornerstone-ondemand-test-user)**  -toohave um equivalente do Britta Simon no Cornerstone OnDemand é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="eb036-145">**[Creating a Cornerstone OnDemand test user](#creating-a-cornerstone-ondemand-test-user)** - toohave a counterpart of Britta Simon in Cornerstone OnDemand that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="eb036-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="eb036-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eb036-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="eb036-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eb036-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb036-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="eb036-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="eb036-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cornerstone OnDemand application.</span></span>

<span data-ttu-id="eb036-150">**tooconfigure AD do Azure-logon único com o Cornerstone OnDemand, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eb036-150">**tooconfigure Azure AD single sign-on with Cornerstone OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb036-151">Em Olá portal do Azure, Olá **Cornerstone OnDemand** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="eb036-151">In hello Azure portal, on hello **Cornerstone OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="eb036-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="eb036-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_samlbase.png)

3. <span data-ttu-id="eb036-155">Em Olá **Cornerstone OnDemand domínio e URLs** , execute Olá etapa a seguir:</span><span class="sxs-lookup"><span data-stu-id="eb036-155">On hello **Cornerstone OnDemand Domain and URLs** section, perform hello following step:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_url.png)

    <span data-ttu-id="eb036-157">a.</span><span class="sxs-lookup"><span data-stu-id="eb036-157">a.</span></span> <span data-ttu-id="eb036-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="eb036-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.csod.com`</span></span>

    <span data-ttu-id="eb036-159">b.</span><span class="sxs-lookup"><span data-stu-id="eb036-159">b.</span></span> <span data-ttu-id="eb036-160">Em **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="eb036-160">In **Identifier** textbox, type a URL using hello following pattern: `https://<company>.csod.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eb036-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="eb036-161">These values are not real.</span></span> <span data-ttu-id="eb036-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="eb036-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="eb036-163">Entre em contato com [equipe de suporte do Cornerstone OnDemand cliente](mailTo:moreinfo@csod.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="eb036-163">Contact [Cornerstone OnDemand Client support team](mailTo:moreinfo@csod.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="eb036-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="eb036-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_certificate.png) 

5. <span data-ttu-id="eb036-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="eb036-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="eb036-168">Em Olá **Cornerstone OnDemand configuração** seção, clique em **configurar Cornerstone OnDemand** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="eb036-168">On hello **Cornerstone OnDemand Configuration** section, click **Configure Cornerstone OnDemand** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="eb036-169">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="eb036-169">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_configure.png) 

7. <span data-ttu-id="eb036-171">tooconfigure logon único no **Cornerstone OnDemand** lado, você precisa toosend Olá baixado **certificado**, **URL de logout** e **único do SAML URL do serviço de logon** muito[equipe de suporte do Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="eb036-171">tooconfigure single sign-on on **Cornerstone OnDemand** side, you need toosend hello downloaded **Certificate**, **Sign-Out URL** and **SAML Single Sign-On Service URL**  too[Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span> <span data-ttu-id="eb036-172">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="eb036-172">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="eb036-173">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="eb036-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="eb036-174">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="eb036-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="eb036-175">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="eb036-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eb036-176">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eb036-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="eb036-177">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="eb036-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="eb036-179">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eb036-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb036-180">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="eb036-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="eb036-182">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="eb036-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="eb036-184">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb036-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="eb036-186">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="eb036-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="eb036-188">a.</span><span class="sxs-lookup"><span data-stu-id="eb036-188">a.</span></span> <span data-ttu-id="eb036-189">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eb036-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="eb036-190">b.</span><span class="sxs-lookup"><span data-stu-id="eb036-190">b.</span></span> <span data-ttu-id="eb036-191">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="eb036-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="eb036-192">c.</span><span class="sxs-lookup"><span data-stu-id="eb036-192">c.</span></span> <span data-ttu-id="eb036-193">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="eb036-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="eb036-194">d.</span><span class="sxs-lookup"><span data-stu-id="eb036-194">d.</span></span> <span data-ttu-id="eb036-195">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="eb036-195">Click **Create**.</span></span>
 
### <a name="creating-a-cornerstone-ondemand-test-user"></a><span data-ttu-id="eb036-196">Como criar um usuário de teste do Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="eb036-196">Creating a Cornerstone OnDemand test user</span></span>

<span data-ttu-id="eb036-197">Em ordem tooenable AD do Azure usuários toolog no Cornerstone OnDemand, eles devem ser provisionados no Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="eb036-197">In order tooenable Azure AD users toolog into Cornerstone OnDemand, they must be provisioned into Cornerstone OnDemand.</span></span> <span data-ttu-id="eb036-198">No caso de saudação do Cornerstone OnDemand, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="eb036-198">In hello case of Cornerstone OnDemand, provisioning is a manual task.</span></span>

<span data-ttu-id="eb036-199">tooconfigure provisionamento de usuário, enviar informações sobre a saudação (por exemplo: nome, Email) sobre o usuário de saudação do AD do Azure você deseja tooprovision toohello [equipe de suporte do Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="eb036-199">tooconfigure user provisioning, send hello information (e.g.: Name, Email) about hello Azure AD user you want tooprovision toohello [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span>

>[!NOTE]
><span data-ttu-id="eb036-200">Você pode usar qualquer ferramenta de criação outros Cornerstone OnDemand usuário conta ou APIs fornecidas pelo Cornerstone OnDemand tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="eb036-200">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="eb036-201">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="eb036-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="eb036-202">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCornerstone sob demanda.</span><span class="sxs-lookup"><span data-stu-id="eb036-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCornerstone OnDemand.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="eb036-204">**tooassign Britta Simon tooCornerstone OnDemand, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="eb036-204">**tooassign Britta Simon tooCornerstone OnDemand, perform hello following steps:**</span></span>

1. <span data-ttu-id="eb036-205">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="eb036-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="eb036-207">Na lista de aplicativos hello, selecione **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="eb036-207">In hello applications list, select **Cornerstone OnDemand**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_app.png) 

3. <span data-ttu-id="eb036-209">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="eb036-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="eb036-211">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="eb036-211">Click **Add** button.</span></span> <span data-ttu-id="eb036-212">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eb036-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="eb036-214">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb036-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="eb036-215">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eb036-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="eb036-216">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="eb036-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="eb036-217">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="eb036-217">Testing single sign-on</span></span>

<span data-ttu-id="eb036-218">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="eb036-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="eb036-219">Quando você clica em bloco Cornerstone OnDemand Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Cornerstone OnDemand aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eb036-219">When you click hello Cornerstone OnDemand tile in hello Access Panel, you should get automatically signed-on tooyour Cornerstone OnDemand application.</span></span>
<span data-ttu-id="eb036-220">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eb036-220">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="eb036-221">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="eb036-221">Additional resources</span></span>

* [<span data-ttu-id="eb036-222">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="eb036-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eb036-223">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eb036-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_203.png

