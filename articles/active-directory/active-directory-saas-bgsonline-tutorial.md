---
title: "Tutorial: integração do Azure Active Directory com o BGS Online | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e unidades Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4fd6b29b-1b46-4fd1-9f5e-16b1c9d892cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: b728606ded7687d424a8175d0602b6b00f398497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bgs-online"></a><span data-ttu-id="c4605-103">Tutorial: Integração do Azure Active Directory ao BGS Online</span><span class="sxs-lookup"><span data-stu-id="c4605-103">Tutorial: Azure Active Directory integration with BGS Online</span></span>

<span data-ttu-id="c4605-104">Neste tutorial, você aprenderá como toointegrate unidades Online com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c4605-104">In this tutorial, you learn how toointegrate BGS Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c4605-105">Integrando unidades Online com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4605-105">Integrating BGS Online with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c4605-106">Você pode controlar no AD do Azure que tenha acesso tooBGS Online</span><span class="sxs-lookup"><span data-stu-id="c4605-106">You can control in Azure AD who has access tooBGS Online</span></span>
- <span data-ttu-id="c4605-107">Você pode habilitar seus usuários tooautomatically get conectado tooBGS on-line (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4605-107">You can enable your users tooautomatically get signed-on tooBGS Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c4605-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c4605-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c4605-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c4605-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4605-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c4605-110">Prerequisites</span></span>

<span data-ttu-id="c4605-111">tooconfigure integração do AD do Azure com unidades Online, você precisará Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4605-111">tooconfigure Azure AD integration with BGS Online, you need hello following items:</span></span>

- <span data-ttu-id="c4605-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4605-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c4605-113">Uma assinatura habilitada para logon único do BGS Online</span><span class="sxs-lookup"><span data-stu-id="c4605-113">A BGS Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c4605-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c4605-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c4605-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c4605-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c4605-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c4605-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c4605-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c4605-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c4605-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c4605-118">Scenario description</span></span>
<span data-ttu-id="c4605-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c4605-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c4605-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c4605-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c4605-121">Adicionando unidades Online da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c4605-121">Adding BGS Online from hello gallery</span></span>
2. <span data-ttu-id="c4605-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4605-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bgs-online-from-hello-gallery"></a><span data-ttu-id="c4605-123">Adicionando unidades Online da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c4605-123">Adding BGS Online from hello gallery</span></span>
<span data-ttu-id="c4605-124">integração de Olá tooconfigure de unidades Online no AD do Azure, você precisa tooadd unidades Online na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c4605-124">tooconfigure hello integration of BGS Online into Azure AD, you need tooadd BGS Online from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c4605-125">**tooadd unidades Online da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c4605-125">**tooadd BGS Online from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4605-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c4605-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c4605-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c4605-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c4605-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c4605-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c4605-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4605-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c4605-133">Na caixa de pesquisa hello, digite **unidades Online**.</span><span class="sxs-lookup"><span data-stu-id="c4605-133">In hello search box, type **BGS Online**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_search.png)

5. <span data-ttu-id="c4605-135">No painel de resultados de saudação, selecione **unidades Online**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c4605-135">In hello results panel, select **BGS Online**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c4605-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4605-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c4605-138">Nesta seção, você configura e testa o logon único do Azure AD com o BGS Online, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c4605-138">In this section, you configure and test Azure AD single sign-on with BGS Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c4605-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em unidades Online é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4605-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BGS Online is tooa user in Azure AD.</span></span> <span data-ttu-id="c4605-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em unidades Online precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c4605-140">In other words, a link relationship between an Azure AD user and hello related user in BGS Online needs toobe established.</span></span>

<span data-ttu-id="c4605-141">Em unidades Online, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4605-141">In BGS Online, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c4605-142">tooconfigure e teste de logon único do AD do Azure com unidades Online, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4605-142">tooconfigure and test Azure AD single sign-on with BGS Online, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c4605-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c4605-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c4605-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c4605-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c4605-145">**[Criar um usuário de teste unidades Online](#creating-a-bgs-online-test-user)**  -toohave um equivalente do Britta Simon em unidades Online que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c4605-145">**[Creating a BGS Online test user](#creating-a-bgs-online-test-user)** - toohave a counterpart of Britta Simon in BGS Online that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c4605-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c4605-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c4605-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c4605-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c4605-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c4605-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c4605-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo unidades Online.</span><span class="sxs-lookup"><span data-stu-id="c4605-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BGS Online application.</span></span>

<span data-ttu-id="c4605-150">**tooconfigure AD do Azure-logon único com unidades Online, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c4605-150">**tooconfigure Azure AD single sign-on with BGS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4605-151">Em Olá portal do Azure, Olá **unidades Online** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c4605-151">In hello Azure portal, on hello **BGS Online** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c4605-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c4605-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_samlbase.png)

3. <span data-ttu-id="c4605-155">Em Olá **domínio Online unidades e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4605-155">On hello **BGS Online Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_url.png)

    <span data-ttu-id="c4605-157">a.</span><span class="sxs-lookup"><span data-stu-id="c4605-157">a.</span></span> <span data-ttu-id="c4605-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4605-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>

    <span data-ttu-id="c4605-159">Para o ambiente de produção, use este padrão `https://<company name>.millwardbrown.report`</span><span class="sxs-lookup"><span data-stu-id="c4605-159">For production environment, use this pattern `https://<company name>.millwardbrown.report`</span></span> 

    <span data-ttu-id="c4605-160">Para o ambiente de teste, use este padrão `https://millwardbrown.marketingtracker.nl/mt5/`</span><span class="sxs-lookup"><span data-stu-id="c4605-160">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/`</span></span>

    <span data-ttu-id="c4605-161">b.</span><span class="sxs-lookup"><span data-stu-id="c4605-161">b.</span></span> <span data-ttu-id="c4605-162">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4605-162">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    
    <span data-ttu-id="c4605-163">Para o ambiente de produção, use este padrão `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="c4605-163">For production environment, use this pattern `https://<company name>.millwardbrown.report/sso/saml/AssertionConsumerService.aspx`</span></span> 
      
    <span data-ttu-id="c4605-164">Para o ambiente de teste, use este padrão `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span><span class="sxs-lookup"><span data-stu-id="c4605-164">For test environment, use this pattern `https://millwardbrown.marketingtracker.nl/mt5/sso/saml/AssertionConsumerService.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c4605-165">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c4605-165">These values are not real.</span></span> <span data-ttu-id="c4605-166">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4605-166">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="c4605-167">Entre em contato com [unidades Online equipe de suporte](mailTo:bgsdashboardteam@millwardbrown.com) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="c4605-167">Contact [BGS Online support team](mailTo:bgsdashboardteam@millwardbrown.com) tooget these values.</span></span>
 

4. <span data-ttu-id="c4605-168">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c4605-168">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_certificate.png) 

5. <span data-ttu-id="c4605-170">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c4605-170">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bgsonline-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c4605-172">Em Olá **configuração Online de unidades** seção, clique em **configurar unidades Online** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="c4605-172">On hello **BGS Online Configuration** section, click **Configure BGS Online** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c4605-173">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="c4605-173">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_configure.png) 

7. <span data-ttu-id="c4605-175">tooconfigure logon único no **unidades Online** lado, você precisa toosend Olá baixado **Metadata XML** e **Single Sign-On URL do serviço SAML** muito[unidades A equipe de suporte online](mailto:bgsdashboardteam@millwardbrown.com).</span><span class="sxs-lookup"><span data-stu-id="c4605-175">tooconfigure single sign-on on **BGS Online** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com).</span></span> 


> [!TIP]
> <span data-ttu-id="c4605-176">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c4605-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c4605-177">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c4605-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c4605-178">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c4605-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c4605-179">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4605-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="c4605-180">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4605-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c4605-182">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c4605-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4605-183">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c4605-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c4605-185">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c4605-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c4605-187">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4605-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c4605-189">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c4605-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bgsonline-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c4605-191">a.</span><span class="sxs-lookup"><span data-stu-id="c4605-191">a.</span></span> <span data-ttu-id="c4605-192">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c4605-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c4605-193">b.</span><span class="sxs-lookup"><span data-stu-id="c4605-193">b.</span></span> <span data-ttu-id="c4605-194">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c4605-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c4605-195">c.</span><span class="sxs-lookup"><span data-stu-id="c4605-195">c.</span></span> <span data-ttu-id="c4605-196">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c4605-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c4605-197">d.</span><span class="sxs-lookup"><span data-stu-id="c4605-197">d.</span></span> <span data-ttu-id="c4605-198">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c4605-198">Click **Create**.</span></span>
 
### <a name="creating-a-bgs-online-test-user"></a><span data-ttu-id="c4605-199">Criando um usuário de teste do BGS Online</span><span class="sxs-lookup"><span data-stu-id="c4605-199">Creating a BGS Online test user</span></span>

<span data-ttu-id="c4605-200">Nesta seção, você criará um usuário chamado Brenda Fernandes no BGS Online.</span><span class="sxs-lookup"><span data-stu-id="c4605-200">In this section, you create a user called Britta Simon in BGS Online.</span></span> <span data-ttu-id="c4605-201">Trabalhar com [unidades Online equipe de suporte](mailto:bgsdashboardteam@millwardbrown.com) tooadd usuários de saudação na plataforma unidades Online hello.</span><span class="sxs-lookup"><span data-stu-id="c4605-201">Work with [BGS Online support team](mailto:bgsdashboardteam@millwardbrown.com) tooadd hello users in hello BGS Online platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c4605-202">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c4605-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c4605-203">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBGS on-line.</span><span class="sxs-lookup"><span data-stu-id="c4605-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBGS Online.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c4605-205">**tooassign Britta Simon tooBGS Online, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c4605-205">**tooassign Britta Simon tooBGS Online, perform hello following steps:**</span></span>

1. <span data-ttu-id="c4605-206">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c4605-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c4605-208">Na lista de aplicativos hello, selecione **unidades Online**.</span><span class="sxs-lookup"><span data-stu-id="c4605-208">In hello applications list, select **BGS Online**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bgsonline-tutorial/tutorial_bgsonline_app.png) 

3. <span data-ttu-id="c4605-210">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c4605-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c4605-212">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c4605-212">Click **Add** button.</span></span> <span data-ttu-id="c4605-213">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4605-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c4605-215">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4605-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c4605-216">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4605-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c4605-217">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c4605-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c4605-218">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c4605-218">Testing single sign-on</span></span>

<span data-ttu-id="c4605-219">Nesta seção, você deve testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4605-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="c4605-220">Quando você clica em bloco unidades Online Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de unidades on-line.</span><span class="sxs-lookup"><span data-stu-id="c4605-220">When you click hello BGS Online tile in hello Access Panel, you should get automatically signed-on tooyour BGS Online application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c4605-221">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c4605-221">Additional resources</span></span>

* [<span data-ttu-id="c4605-222">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c4605-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c4605-223">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c4605-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bgsonline-tutorial/tutorial_general_203.png

