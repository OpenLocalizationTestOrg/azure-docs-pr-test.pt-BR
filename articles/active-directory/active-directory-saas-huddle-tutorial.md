---
title: "Tutorial: Integração do Azure Active Directory ao Huddle | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Huddle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0b2f6c4d839943cdd07699a1ff95dc8f90505699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="efe4e-103">Tutorial: integração do Active Directory do Azure ao Huddle</span><span class="sxs-lookup"><span data-stu-id="efe4e-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="efe4e-104">Neste tutorial, você aprenderá como toointegrate Huddle com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="efe4e-104">In this tutorial, you learn how toointegrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="efe4e-105">Integrando o Huddle com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="efe4e-105">Integrating Huddle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="efe4e-106">Você pode controlar no AD do Azure que tenha acesso tooHuddle</span><span class="sxs-lookup"><span data-stu-id="efe4e-106">You can control in Azure AD who has access tooHuddle</span></span>
- <span data-ttu-id="efe4e-107">Você pode habilitar seu usuários tooautomatically get conectado tooHuddle (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="efe4e-107">You can enable your users tooautomatically get signed-on tooHuddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="efe4e-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="efe4e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="efe4e-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="efe4e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="efe4e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="efe4e-110">Prerequisites</span></span>

<span data-ttu-id="efe4e-111">integração de tooconfigure AD do Azure com o Huddle, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="efe4e-111">tooconfigure Azure AD integration with Huddle, you need hello following items:</span></span>

- <span data-ttu-id="efe4e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="efe4e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="efe4e-113">Uma assinatura habilitada para logon único do Huddle</span><span class="sxs-lookup"><span data-stu-id="efe4e-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="efe4e-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="efe4e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="efe4e-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="efe4e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="efe4e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="efe4e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="efe4e-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="efe4e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="efe4e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="efe4e-118">Scenario description</span></span>

<span data-ttu-id="efe4e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="efe4e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="efe4e-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="efe4e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="efe4e-121">Adicionando Huddle da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="efe4e-121">Adding Huddle from hello gallery</span></span>
2. <span data-ttu-id="efe4e-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="efe4e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-hello-gallery"></a><span data-ttu-id="efe4e-123">Adicionando Huddle da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="efe4e-123">Adding Huddle from hello gallery</span></span>
<span data-ttu-id="efe4e-124">integração de saudação do tooconfigure do Huddle no AD do Azure, você precisa tooadd Huddle da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="efe4e-124">tooconfigure hello integration of Huddle into Azure AD, you need tooadd Huddle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="efe4e-125">**tooadd Huddle da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="efe4e-125">**tooadd Huddle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="efe4e-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="efe4e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="efe4e-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="efe4e-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="efe4e-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="efe4e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="efe4e-133">Na caixa de pesquisa hello, digite **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-133">In hello search box, type **Huddle**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="efe4e-135">No painel de resultados de saudação, selecione **Huddle**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="efe4e-135">In hello results panel, select **Huddle**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="efe4e-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="efe4e-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="efe4e-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Huddle, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="efe4e-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="efe4e-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Huddle é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="efe4e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Huddle is tooa user in Azure AD.</span></span> <span data-ttu-id="efe4e-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e hello relacionados ao usuário no Huddle necessidades toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="efe4e-140">In other words, a link relationship between an Azure AD user and hello related user in Huddle needs toobe established.</span></span>

<span data-ttu-id="efe4e-141">No Huddle, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="efe4e-141">In Huddle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="efe4e-142">tooconfigure e teste de logon único do AD do Azure com o Huddle, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="efe4e-142">tooconfigure and test Azure AD single sign-on with Huddle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="efe4e-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="efe4e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>

2. <span data-ttu-id="efe4e-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="efe4e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="efe4e-145">**[Criar um usuário de teste do Huddle](#creating-a-huddle-test-user)**  -toohave um equivalente do Britta Simon no Huddle é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="efe4e-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - toohave a counterpart of Britta Simon in Huddle that is linked toohello Azure AD representation of user.</span></span>

4. <span data-ttu-id="efe4e-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="efe4e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>

5. <span data-ttu-id="efe4e-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="efe4e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="efe4e-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="efe4e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="efe4e-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Huddle.</span><span class="sxs-lookup"><span data-stu-id="efe4e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="efe4e-150">**tooconfigure logon único do AD do Azure com o Huddle, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="efe4e-150">**tooconfigure Azure AD single sign-on with Huddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="efe4e-151">Em Olá portal do Azure, Olá **Huddle** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-151">In hello Azure portal, on hello **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="efe4e-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="efe4e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="efe4e-155">Em Olá **Huddle domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="efe4e-155">On hello **Huddle Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="efe4e-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="efe4e-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="efe4e-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="efe4e-158">This value is not real.</span></span> <span data-ttu-id="efe4e-159">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="efe4e-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="efe4e-160">Entre em contato com [equipe de suporte do Huddle cliente](https://huddle.zendesk.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="efe4e-160">Contact [Huddle Client support team](https://huddle.zendesk.com) tooget this value.</span></span> 

4. <span data-ttu-id="efe4e-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="efe4e-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="efe4e-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="efe4e-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="efe4e-165">Em Olá **Huddle configuração** seção, clique em **configurar Huddle** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="efe4e-165">On hello **Huddle Configuration** section, click **Configure Huddle** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="efe4e-166">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="efe4e-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    ![Configurar Logon Único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="efe4e-168">tooconfigure logon único no lado do Huddle, você precisa toosend Olá baixado **certificado**, **Single Sign-On URL do serviço SAML**, e **ID da entidade SAML** muito[Equipe de suporte do huddle cliente](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="efe4e-168">tooconfigure single sign-on on Huddle side, you need toosend hello downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="efe4e-169">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="efe4e-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="efe4e-170">O logon único precisa toobe habilitado pela equipe de suporte do Huddle hello.</span><span class="sxs-lookup"><span data-stu-id="efe4e-170">Single sign-on needs toobe enabled by hello Huddle support team.</span></span> <span data-ttu-id="efe4e-171">Você recebe uma notificação ao Olá configuração foi concluída.</span><span class="sxs-lookup"><span data-stu-id="efe4e-171">You get a notification when hello configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="efe4e-172">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="efe4e-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="efe4e-173">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="efe4e-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="efe4e-174">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="efe4e-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="efe4e-175">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="efe4e-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="efe4e-176">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="efe4e-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="efe4e-178">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="efe4e-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="efe4e-179">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="efe4e-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="efe4e-181">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="efe4e-183">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="efe4e-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="efe4e-185">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="efe4e-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="efe4e-187">a.</span><span class="sxs-lookup"><span data-stu-id="efe4e-187">a.</span></span> <span data-ttu-id="efe4e-188">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="efe4e-189">b.</span><span class="sxs-lookup"><span data-stu-id="efe4e-189">b.</span></span> <span data-ttu-id="efe4e-190">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="efe4e-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="efe4e-191">c.</span><span class="sxs-lookup"><span data-stu-id="efe4e-191">c.</span></span> <span data-ttu-id="efe4e-192">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="efe4e-193">d.</span><span class="sxs-lookup"><span data-stu-id="efe4e-193">d.</span></span> <span data-ttu-id="efe4e-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="efe4e-195">Criação de um usuário de teste do Huddle</span><span class="sxs-lookup"><span data-stu-id="efe4e-195">Creating a Huddle test user</span></span>

<span data-ttu-id="efe4e-196">tooenable AD do Azure usuários toolog em tooHuddle, eles devem ser provisionados no Huddle.</span><span class="sxs-lookup"><span data-stu-id="efe4e-196">tooenable Azure AD users toolog in tooHuddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="efe4e-197">No caso de saudação do Huddle, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="efe4e-197">In hello case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="efe4e-198">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="efe4e-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="efe4e-199">Faça logon no tooyour **Huddle** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="efe4e-199">Log in tooyour **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="efe4e-200">Clique em **Espaço de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="efe4e-201">Clique em **Pessoas \> Convidar Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="efe4e-202">![Pessoas](./media/active-directory-saas-huddle-tutorial/IC787838.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="efe4e-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="efe4e-203">Em Olá **criar um novo convite** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="efe4e-203">In hello **Create a new invitation** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="efe4e-204">![Novo Convite](./media/active-directory-saas-huddle-tutorial/IC787839.png "Novo Convite")</span><span class="sxs-lookup"><span data-stu-id="efe4e-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="efe4e-205">a.</span><span class="sxs-lookup"><span data-stu-id="efe4e-205">a.</span></span> <span data-ttu-id="efe4e-206">Em Olá **escolha um toojoin de pessoas team tooinvite** lista, selecione **equipe**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-206">In hello **Choose a team tooinvite people toojoin** list, select **team**.</span></span>

   <span data-ttu-id="efe4e-207">b.</span><span class="sxs-lookup"><span data-stu-id="efe4e-207">b.</span></span> <span data-ttu-id="efe4e-208">Saudação de tipo **endereço de Email** de um AD do Azure válidas de conta deseja tooprovision muito**informe o endereço de email para as pessoas que deseja tooinvite** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="efe4e-208">Type hello **Email Address** of a valid Azure AD account you want tooprovision in too**Enter email address for people you'd like tooinvite** textbox.</span></span>

   <span data-ttu-id="efe4e-209">c.</span><span class="sxs-lookup"><span data-stu-id="efe4e-209">c.</span></span> <span data-ttu-id="efe4e-210">Clique em **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="efe4e-211">Olá conta do AD do Azure proprietário receberá um email com uma conta de saudação do link tooconfirm antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="efe4e-211">hello Azure AD account holder will receive an email including a link tooconfirm hello account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="efe4e-212">Você pode usar qualquer ferramenta de criação outros Huddle usuário conta ou APIs fornecidas pelo Huddle tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="efe4e-212">You can use any other Huddle user account creation tools or APIs provided by Huddle tooprovision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="efe4e-213">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="efe4e-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="efe4e-214">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooHuddle.</span><span class="sxs-lookup"><span data-stu-id="efe4e-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHuddle.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="efe4e-216">**tooassign Britta Simon tooHuddle, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="efe4e-216">**tooassign Britta Simon tooHuddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="efe4e-217">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="efe4e-219">Na lista de aplicativos hello, selecione **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-219">In hello applications list, select **Huddle**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="efe4e-221">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="efe4e-223">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="efe4e-223">Click **Add** button.</span></span> <span data-ttu-id="efe4e-224">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="efe4e-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="efe4e-226">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="efe4e-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="efe4e-227">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="efe4e-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="efe4e-228">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="efe4e-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="efe4e-229">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="efe4e-229">Testing single sign-on</span></span>

<span data-ttu-id="efe4e-230">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="efe4e-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="efe4e-231">Quando você clica em bloco Huddle Olá Olá painel de acesso, você deve obter automaticamente a página de logon do aplicativo do Huddle.</span><span class="sxs-lookup"><span data-stu-id="efe4e-231">When you click hello Huddle tile in hello Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="efe4e-232">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="efe4e-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="efe4e-233">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="efe4e-233">Additional resources</span></span>

* [<span data-ttu-id="efe4e-234">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="efe4e-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="efe4e-235">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="efe4e-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
