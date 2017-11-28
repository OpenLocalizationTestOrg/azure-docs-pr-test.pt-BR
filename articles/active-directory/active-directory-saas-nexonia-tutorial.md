---
title: "Tutorial: Integração do Azure Active Directory ao Nexonia | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Nexonia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 3778804084a7989414260bae5654cf76e9ccca6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="529e1-103">Tutorial: Integração do Azure Active Directory ao Nexonia</span><span class="sxs-lookup"><span data-stu-id="529e1-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="529e1-104">Neste tutorial, você aprenderá como toointegrate Nexonia com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="529e1-104">In this tutorial, you learn how toointegrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="529e1-105">Integrando Nexonia com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="529e1-105">Integrating Nexonia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="529e1-106">Você pode controlar no AD do Azure que tenha acesso tooNexonia</span><span class="sxs-lookup"><span data-stu-id="529e1-106">You can control in Azure AD who has access tooNexonia</span></span>
- <span data-ttu-id="529e1-107">Você pode habilitar seu usuários tooautomatically get conectado tooNexonia (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="529e1-107">You can enable your users tooautomatically get signed-on tooNexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="529e1-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="529e1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="529e1-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte.</span><span class="sxs-lookup"><span data-stu-id="529e1-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="529e1-110">[O que é o acesso a aplicativos e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="529e1-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="529e1-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="529e1-111">Prerequisites</span></span>

<span data-ttu-id="529e1-112">tooconfigure integração do AD do Azure com Nexonia, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="529e1-112">tooconfigure Azure AD integration with Nexonia, you need hello following items:</span></span>

- <span data-ttu-id="529e1-113">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="529e1-113">An Azure AD subscription</span></span>
- <span data-ttu-id="529e1-114">Uma assinatura do Nexonia habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="529e1-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="529e1-115">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="529e1-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="529e1-116">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="529e1-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="529e1-117">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="529e1-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="529e1-118">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="529e1-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="529e1-119">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="529e1-119">Scenario description</span></span>
<span data-ttu-id="529e1-120">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="529e1-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="529e1-121">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="529e1-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="529e1-122">Adicionando Nexonia da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="529e1-122">Adding Nexonia from hello gallery</span></span>
2. <span data-ttu-id="529e1-123">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="529e1-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-hello-gallery"></a><span data-ttu-id="529e1-124">Adicionando Nexonia da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="529e1-124">Adding Nexonia from hello gallery</span></span>
<span data-ttu-id="529e1-125">integração de saudação tooconfigure de Nexonia no AD do Azure, você precisa tooadd Nexonia da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="529e1-125">tooconfigure hello integration of Nexonia into Azure AD, you need tooadd Nexonia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="529e1-126">**tooadd Nexonia da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="529e1-126">**tooadd Nexonia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="529e1-127">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="529e1-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="529e1-129">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="529e1-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="529e1-130">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="529e1-130">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="529e1-132">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="529e1-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="529e1-134">Na caixa de pesquisa hello, digite **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="529e1-134">In hello search box, type **Nexonia**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="529e1-136">No painel de resultados de saudação, selecione **Nexonia**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="529e1-136">In hello results panel, select **Nexonia**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="529e1-138">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="529e1-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="529e1-139">Nesta seção, você configurará e testará o logon único do Azure AD com o Nexonia, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="529e1-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="529e1-140">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Nexonia é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="529e1-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nexonia is tooa user in Azure AD.</span></span> <span data-ttu-id="529e1-141">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Nexonia precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="529e1-141">In other words, a link relationship between an Azure AD user and hello related user in Nexonia needs toobe established.</span></span>

<span data-ttu-id="529e1-142">Nexonia, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="529e1-142">In Nexonia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="529e1-143">tooconfigure e teste de logon único do AD do Azure com Nexonia, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="529e1-143">tooconfigure and test Azure AD single sign-on with Nexonia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="529e1-144">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="529e1-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="529e1-145">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="529e1-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="529e1-146">**[Criar um usuário de teste Nexonia](#creating-a-nexonia-test-user)**  -toohave um equivalente do Britta Simon em Nexonia é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="529e1-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - toohave a counterpart of Britta Simon in Nexonia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="529e1-147">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="529e1-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="529e1-148">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="529e1-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="529e1-149">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="529e1-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="529e1-150">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Nexonia.</span><span class="sxs-lookup"><span data-stu-id="529e1-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="529e1-151">Se você tiver problemas na integração hello e consulte isso [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) para guia de solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="529e1-151">If you have issues in hello integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="529e1-152">Se você ainda não encontrou solução hello, em seguida, gere solicitação de suporte de saudação do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="529e1-152">If you still have not found hello solution, then raise hello support request from Azure portal.</span></span>

<span data-ttu-id="529e1-153">**tooconfigure AD do Azure-logon único com Nexonia, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="529e1-153">**tooconfigure Azure AD single sign-on with Nexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="529e1-154">Em Olá portal do Azure, Olá **Nexonia** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="529e1-154">In hello Azure portal, on hello **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="529e1-156">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="529e1-156">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="529e1-158">Em Olá **Nexonia domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="529e1-158">On hello **Nexonia Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="529e1-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="529e1-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="529e1-161">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="529e1-161">This value is not real.</span></span> <span data-ttu-id="529e1-162">Atualize esse valor com hello URL de resposta real.</span><span class="sxs-lookup"><span data-stu-id="529e1-162">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="529e1-163">Entre em contato com [Nexonia a equipe de suporte](https://nexonia.zendesk.com/hc/requests/new) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="529e1-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooget this value.</span></span> 


4. <span data-ttu-id="529e1-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="529e1-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="529e1-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="529e1-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="529e1-168">Em Olá **Nexonia configuração** seção, clique em **configurar Nexonia** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="529e1-168">On hello **Nexonia Configuration** section, click **Configure Nexonia** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="529e1-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="529e1-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="529e1-171">tooget SSO configurado para o seu aplicativo, entre em contato com [Nexonia a equipe de suporte](https://nexonia.zendesk.com/hc/requests/new) e fornecê-los com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="529e1-171">tooget SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with hello following:</span></span>

    <span data-ttu-id="529e1-172">• Olá baixado **certificado**</span><span class="sxs-lookup"><span data-stu-id="529e1-172">• hello downloaded **certificate**</span></span>

    <span data-ttu-id="529e1-173">• Olá **ID de entidade de SAML**</span><span class="sxs-lookup"><span data-stu-id="529e1-173">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="529e1-174">• Olá **Single Sign-On URL do serviço SAML**</span><span class="sxs-lookup"><span data-stu-id="529e1-174">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="529e1-175">• Olá **URL de logout**</span><span class="sxs-lookup"><span data-stu-id="529e1-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="529e1-176">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="529e1-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="529e1-177">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="529e1-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="529e1-178">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="529e1-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="529e1-179">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="529e1-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="529e1-180">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="529e1-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="529e1-182">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="529e1-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="529e1-183">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="529e1-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="529e1-185">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="529e1-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="529e1-187">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="529e1-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="529e1-189">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="529e1-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="529e1-191">a.</span><span class="sxs-lookup"><span data-stu-id="529e1-191">a.</span></span> <span data-ttu-id="529e1-192">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="529e1-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="529e1-193">b.</span><span class="sxs-lookup"><span data-stu-id="529e1-193">b.</span></span> <span data-ttu-id="529e1-194">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="529e1-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="529e1-195">c.</span><span class="sxs-lookup"><span data-stu-id="529e1-195">c.</span></span> <span data-ttu-id="529e1-196">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="529e1-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="529e1-197">d.</span><span class="sxs-lookup"><span data-stu-id="529e1-197">d.</span></span> <span data-ttu-id="529e1-198">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="529e1-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="529e1-199">Criar um usuário de teste do Nexonia</span><span class="sxs-lookup"><span data-stu-id="529e1-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="529e1-200">Nesta seção, você criará um usuário chamado Brenda Fernandes no Nexonia.</span><span class="sxs-lookup"><span data-stu-id="529e1-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="529e1-201">Trabalhar com [Nexonia a equipe de suporte](https://nexonia.zendesk.com/hc/requests/new) tooadd usuários de saudação na plataforma de Nexonia hello.</span><span class="sxs-lookup"><span data-stu-id="529e1-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooadd hello users in hello Nexonia platform.</span></span> <span data-ttu-id="529e1-202">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="529e1-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="529e1-203">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="529e1-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="529e1-204">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooNexonia.</span><span class="sxs-lookup"><span data-stu-id="529e1-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNexonia.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="529e1-206">**tooassign Britta Simon tooNexonia, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="529e1-206">**tooassign Britta Simon tooNexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="529e1-207">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="529e1-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="529e1-209">Na lista de aplicativos hello, selecione **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="529e1-209">In hello applications list, select **Nexonia**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="529e1-211">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="529e1-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="529e1-213">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="529e1-213">Click **Add** button.</span></span> <span data-ttu-id="529e1-214">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="529e1-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="529e1-216">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="529e1-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="529e1-217">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="529e1-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="529e1-218">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="529e1-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="529e1-219">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="529e1-219">Testing single sign-on</span></span>

<span data-ttu-id="529e1-220">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="529e1-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="529e1-221">Quando você clica em bloco Nexonia Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Nexonia aplicativo.</span><span class="sxs-lookup"><span data-stu-id="529e1-221">When you click hello Nexonia tile in hello Access Panel, you should get automatically signed-on tooyour Nexonia application.</span></span>
<span data-ttu-id="529e1-222">Para saber mais sobre o Painel de Acesso, veja [Introdução ao Painel de Acesso](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="529e1-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="529e1-223">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="529e1-223">Additional resources</span></span>

* [<span data-ttu-id="529e1-224">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="529e1-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="529e1-225">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="529e1-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

