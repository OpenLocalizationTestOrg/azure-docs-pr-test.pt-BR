---
title: "Tutorial: integração do Azure Active Directory ao Cherwell | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Cherwell."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad891f99-179e-4487-834d-35f3bc01c1ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: jeedes
ms.openlocfilehash: a67b3d346a6f7b43a7e87fb4d9c533f9363f2e02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cherwell"></a><span data-ttu-id="08de8-103">Tutorial: Integração do Active Directory do Azure ao Cherwell</span><span class="sxs-lookup"><span data-stu-id="08de8-103">Tutorial: Azure Active Directory integration with Cherwell</span></span>

<span data-ttu-id="08de8-104">Neste tutorial, você aprenderá como toointegrate Cherwell com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="08de8-104">In this tutorial, you learn how toointegrate Cherwell with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="08de8-105">Integrando o Cherwell com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="08de8-105">Integrating Cherwell with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="08de8-106">Você pode controlar no AD do Azure que tenha acesso tooCherwell</span><span class="sxs-lookup"><span data-stu-id="08de8-106">You can control in Azure AD who has access tooCherwell</span></span>
- <span data-ttu-id="08de8-107">Você pode habilitar seu usuários tooautomatically get conectado tooCherwell (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08de8-107">You can enable your users tooautomatically get signed-on tooCherwell (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="08de8-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="08de8-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="08de8-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="08de8-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="08de8-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="08de8-110">Prerequisites</span></span>

<span data-ttu-id="08de8-111">tooconfigure integração do AD do Azure com o Cherwell, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="08de8-111">tooconfigure Azure AD integration with Cherwell, you need hello following items:</span></span>

- <span data-ttu-id="08de8-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08de8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="08de8-113">Uma assinatura habilitada para logon único do Cherwell</span><span class="sxs-lookup"><span data-stu-id="08de8-113">A Cherwell single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="08de8-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="08de8-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="08de8-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="08de8-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="08de8-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="08de8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="08de8-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="08de8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="08de8-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="08de8-118">Scenario description</span></span>
<span data-ttu-id="08de8-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="08de8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="08de8-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="08de8-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="08de8-121">Adicionando Cherwell da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="08de8-121">Adding Cherwell from hello gallery</span></span>
2. <span data-ttu-id="08de8-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08de8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cherwell-from-hello-gallery"></a><span data-ttu-id="08de8-123">Adicionando Cherwell da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="08de8-123">Adding Cherwell from hello gallery</span></span>
<span data-ttu-id="08de8-124">integração de saudação tooconfigure do Cherwell no AD do Azure, você precisa tooadd Cherwell da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="08de8-124">tooconfigure hello integration of Cherwell into Azure AD, you need tooadd Cherwell from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="08de8-125">**tooadd Cherwell da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="08de8-125">**tooadd Cherwell from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="08de8-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="08de8-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="08de8-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="08de8-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="08de8-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="08de8-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="08de8-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08de8-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="08de8-133">Na caixa de pesquisa hello, digite **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="08de8-133">In hello search box, type **Cherwell**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_search.png)

5. <span data-ttu-id="08de8-135">No painel de resultados de saudação, selecione **Cherwell**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="08de8-135">In hello results panel, select **Cherwell**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="08de8-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08de8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="08de8-138">Nesta seção, você configura e testa o logon único do Azure AD com o Cherwell, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="08de8-138">In this section, you configure and test Azure AD single sign-on with Cherwell based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="08de8-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Cherwell é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="08de8-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cherwell is tooa user in Azure AD.</span></span> <span data-ttu-id="08de8-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Cherwell precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="08de8-140">In other words, a link relationship between an Azure AD user and hello related user in Cherwell needs toobe established.</span></span>

<span data-ttu-id="08de8-141">No Cherwell, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="08de8-141">In Cherwell, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="08de8-142">tooconfigure e teste de logon único do AD do Azure com o Cherwell, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="08de8-142">tooconfigure and test Azure AD single sign-on with Cherwell, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="08de8-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="08de8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="08de8-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="08de8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="08de8-145">**[Criar um usuário de teste do Cherwell](#creating-a-cherwell-test-user)**  -toohave um equivalente do Britta Simon no Cherwell é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="08de8-145">**[Creating a Cherwell test user](#creating-a-cherwell-test-user)** - toohave a counterpart of Britta Simon in Cherwell that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="08de8-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="08de8-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="08de8-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="08de8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="08de8-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="08de8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="08de8-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Cherwell.</span><span class="sxs-lookup"><span data-stu-id="08de8-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cherwell application.</span></span>

<span data-ttu-id="08de8-150">**tooconfigure AD do Azure-logon único com o Cherwell, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="08de8-150">**tooconfigure Azure AD single sign-on with Cherwell, perform hello following steps:**</span></span>

1. <span data-ttu-id="08de8-151">Em Olá portal do Azure, Olá **Cherwell** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="08de8-151">In hello Azure portal, on hello **Cherwell** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="08de8-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="08de8-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_samlbase.png)

3. <span data-ttu-id="08de8-155">Em Olá **Cherwell domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="08de8-155">On hello **Cherwell Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_url.png)

    <span data-ttu-id="08de8-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.cherwellondemand.com/cherwellclient`</span><span class="sxs-lookup"><span data-stu-id="08de8-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.cherwellondemand.com/cherwellclient`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="08de8-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="08de8-158">This value is not real.</span></span> <span data-ttu-id="08de8-159">Atualize esse valor com a URL de logon real hello.</span><span class="sxs-lookup"><span data-stu-id="08de8-159">Update this value with hello actual Sign-on URL.</span></span> <span data-ttu-id="08de8-160">Entre em contato com [equipe de suporte do Cherwell](https://csm.cherwell.com/contact) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="08de8-160">Contact [Cherwell support team](https://csm.cherwell.com/contact) tooget this value.</span></span>
 
4. <span data-ttu-id="08de8-161">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="08de8-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_certificate.png) 

5. <span data-ttu-id="08de8-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="08de8-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cherwell-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="08de8-165">Em Olá **Cherwell configuração** seção, clique em **configurar Cherwell** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="08de8-165">On hello **Cherwell Configuration** section, click **Configure Cherwell** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="08de8-166">Saudação de cópia **ID da entidade SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="08de8-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_configure.png) 

7. <span data-ttu-id="08de8-168">tooconfigure logon único no **Cherwell** lado, você precisa toosend Olá baixado **certificado (Base64)**, **Single Sign-On URL do serviço SAML**, e  **ID da entidade SAML** muito[equipe de suporte do Cherwell](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="08de8-168">tooconfigure single sign-on on **Cherwell** side, you need toosend hello downloaded **Certificate (Base64)**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Cherwell support team](https://csm.cherwell.com/contact).</span></span> 

    >[!NOTE]
    ><span data-ttu-id="08de8-169">Sua equipe de suporte do Cherwell tem toodo Olá configuração real do SSO.</span><span class="sxs-lookup"><span data-stu-id="08de8-169">Your Cherwell support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="08de8-170">Você receberá uma notificação quando o SSO tiver sido habilitado para sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="08de8-170">You will get a notification when SSO has been enabled for your subscription.</span></span>
    > 
    
> [!TIP]
> <span data-ttu-id="08de8-171">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="08de8-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="08de8-172">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="08de8-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="08de8-173">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="08de8-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="08de8-174">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08de8-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="08de8-175">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="08de8-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="08de8-177">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="08de8-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="08de8-178">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="08de8-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cherwell-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="08de8-180">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="08de8-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cherwell-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="08de8-182">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="08de8-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cherwell-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="08de8-184">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="08de8-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-cherwell-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="08de8-186">a.</span><span class="sxs-lookup"><span data-stu-id="08de8-186">a.</span></span> <span data-ttu-id="08de8-187">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="08de8-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="08de8-188">b.</span><span class="sxs-lookup"><span data-stu-id="08de8-188">b.</span></span> <span data-ttu-id="08de8-189">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="08de8-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="08de8-190">c.</span><span class="sxs-lookup"><span data-stu-id="08de8-190">c.</span></span> <span data-ttu-id="08de8-191">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="08de8-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="08de8-192">d.</span><span class="sxs-lookup"><span data-stu-id="08de8-192">d.</span></span> <span data-ttu-id="08de8-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="08de8-193">Click **Create**.</span></span>
 
### <a name="creating-a-cherwell-test-user"></a><span data-ttu-id="08de8-194">Criando um usuário de teste do Cherwell</span><span class="sxs-lookup"><span data-stu-id="08de8-194">Creating a Cherwell test user</span></span>

<span data-ttu-id="08de8-195">tooenable AD do Azure usuários toolog em tooCherwell, eles devem ser provisionados no Cherwell.</span><span class="sxs-lookup"><span data-stu-id="08de8-195">tooenable Azure AD users toolog in tooCherwell, they must be provisioned into Cherwell.</span></span>

<span data-ttu-id="08de8-196">No caso de saudação de Cherwell, as contas de usuário Olá necessário toobe criado por seu [equipe de suporte do Cherwell](https://csm.cherwell.com/contact).</span><span class="sxs-lookup"><span data-stu-id="08de8-196">In hello case of Cherwell, hello user accounts need toobe created by your [Cherwell support team](https://csm.cherwell.com/contact).</span></span>

>[!NOTE]
><span data-ttu-id="08de8-197">Você pode usar qualquer ferramenta de criação outros Cherwell usuário conta ou APIs fornecidas pelo Cherwell tooprovision Azure Active Directory as contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="08de8-197">You can use any other Cherwell user account creation tools or APIs provided by Cherwell tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="08de8-198">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="08de8-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="08de8-199">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCherwell.</span><span class="sxs-lookup"><span data-stu-id="08de8-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCherwell.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="08de8-201">**tooassign Britta Simon tooCherwell, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="08de8-201">**tooassign Britta Simon tooCherwell, perform hello following steps:**</span></span>

1. <span data-ttu-id="08de8-202">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="08de8-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="08de8-204">Na lista de aplicativos hello, selecione **Cherwell**.</span><span class="sxs-lookup"><span data-stu-id="08de8-204">In hello applications list, select **Cherwell**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-cherwell-tutorial/tutorial_cherwell_app.png) 

3. <span data-ttu-id="08de8-206">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="08de8-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="08de8-208">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="08de8-208">Click **Add** button.</span></span> <span data-ttu-id="08de8-209">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08de8-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="08de8-211">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="08de8-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="08de8-212">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08de8-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="08de8-213">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="08de8-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="08de8-214">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="08de8-214">Testing single sign-on</span></span>

<span data-ttu-id="08de8-215">Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="08de8-215">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="08de8-216">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="08de8-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="08de8-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="08de8-217">Additional resources</span></span>

* [<span data-ttu-id="08de8-218">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="08de8-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="08de8-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="08de8-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cherwell-tutorial/tutorial_general_203.png

