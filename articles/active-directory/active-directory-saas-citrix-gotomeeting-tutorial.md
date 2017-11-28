---
title: "Tutorial: integração do Azure Active Directory ao Citrix GoToMeeting | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7d7897f6-b88e-4dd5-8f3a-e612337b1413
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 46a5da7504806202a5ec29f73c504e772c61bc2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-citrix-gotomeeting"></a><span data-ttu-id="c27de-103">Tutorial: integração do Active Directory do Azure ao Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="c27de-103">Tutorial: Azure Active Directory integration with Citrix GoToMeeting</span></span>

<span data-ttu-id="c27de-104">Neste tutorial, você aprenderá como toointegrate Citrix GoToMeeting com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c27de-104">In this tutorial, you learn how toointegrate Citrix GoToMeeting with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c27de-105">Integração do Citrix GoToMeeting com o Azure AD oferece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c27de-105">Integrating Citrix GoToMeeting with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c27de-106">Você pode controlar no AD do Azure que tenha acesso tooCitrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="c27de-106">You can control in Azure AD who has access tooCitrix GoToMeeting</span></span>
- <span data-ttu-id="c27de-107">Você pode habilitar seu usuários tooautomatically get conectado tooCitrix GoToMeeting (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c27de-107">You can enable your users tooautomatically get signed-on tooCitrix GoToMeeting (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c27de-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c27de-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c27de-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c27de-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c27de-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c27de-110">Prerequisites</span></span>

<span data-ttu-id="c27de-111">tooconfigure integração do Azure AD com Citrix GoToMeeting, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c27de-111">tooconfigure Azure AD integration with Citrix GoToMeeting, you need hello following items:</span></span>

- <span data-ttu-id="c27de-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c27de-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c27de-113">Uma assinatura do Citrix GoToMeeting habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="c27de-113">A Citrix GoToMeeting single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c27de-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c27de-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c27de-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c27de-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c27de-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c27de-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c27de-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c27de-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c27de-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c27de-118">Scenario description</span></span>
<span data-ttu-id="c27de-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c27de-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c27de-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c27de-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c27de-121">Adicionando Citrix GoToMeeting da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c27de-121">Adding Citrix GoToMeeting from hello gallery</span></span>
2. <span data-ttu-id="c27de-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c27de-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-citrix-gotomeeting-from-hello-gallery"></a><span data-ttu-id="c27de-123">Adicionando Citrix GoToMeeting da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c27de-123">Adding Citrix GoToMeeting from hello gallery</span></span>
<span data-ttu-id="c27de-124">integração de saudação tooconfigure do Citrix GoToMeeting no AD do Azure, você precisa tooadd Citrix GoToMeeting da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c27de-124">tooconfigure hello integration of Citrix GoToMeeting into Azure AD, you need tooadd Citrix GoToMeeting from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c27de-125">**tooadd Citrix GoToMeeting da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c27de-125">**tooadd Citrix GoToMeeting from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c27de-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c27de-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c27de-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c27de-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c27de-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c27de-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c27de-131">Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c27de-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c27de-133">Na caixa de pesquisa hello, digite **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="c27de-133">In hello search box, type **Citrix GoToMeeting**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_search.png)

5. <span data-ttu-id="c27de-135">No painel de resultados de saudação, selecione **Citrix GoToMeeting**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c27de-135">In hello results panel, select **Citrix GoToMeeting**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c27de-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c27de-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c27de-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Citrix GoToMeeting com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="c27de-138">In this section, you configure and test Azure AD single sign-on with Citrix GoToMeeting based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c27de-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Citrix GoToMeeting é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c27de-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Citrix GoToMeeting is tooa user in Azure AD.</span></span> <span data-ttu-id="c27de-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Citrix GoToMeeting precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c27de-140">In other words, a link relationship between an Azure AD user and hello related user in Citrix GoToMeeting needs toobe established.</span></span>

<span data-ttu-id="c27de-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="c27de-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Citrix GoToMeeting.</span></span>

<span data-ttu-id="c27de-142">tooconfigure e teste de logon único do Azure AD com Citrix GoToMeeting, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c27de-142">tooconfigure and test Azure AD single sign-on with Citrix GoToMeeting, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c27de-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c27de-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c27de-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c27de-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c27de-145">**[Criar um usuário de teste do Citrix GoToMeeting](#creating-a-citrix-gotomeeting-test-user)**  -toohave um equivalente do Britta Simon no Citrix GoToMeeting que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c27de-145">**[Creating a Citrix GoToMeeting test user](#creating-a-citrix-gotomeeting-test-user)** - toohave a counterpart of Britta Simon in Citrix GoToMeeting that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c27de-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c27de-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c27de-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c27de-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c27de-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c27de-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c27de-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="c27de-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Citrix GoToMeeting application.</span></span>

<span data-ttu-id="c27de-150">**tooconfigure AD do Azure-logon único com o Citrix GoToMeeting, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c27de-150">**tooconfigure Azure AD single sign-on with Citrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="c27de-151">Em Olá portal do Azure, Olá **Citrix GoToMeeting** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c27de-151">In hello Azure portal, on hello **Citrix GoToMeeting** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c27de-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c27de-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_samlbase.png)

3. <span data-ttu-id="c27de-155">Em Olá **URLs e Citrix GoToMeeting domínio** seção tooperform sem necessidade de todas as etapas.</span><span class="sxs-lookup"><span data-stu-id="c27de-155">On hello **Citrix GoToMeeting Domain and URLs** section, no need tooperform any steps.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_url.png)


3. <span data-ttu-id="c27de-157">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c27de-157">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_certificate.png) 

4. <span data-ttu-id="c27de-159">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c27de-159">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_400.png)
    
5. <span data-ttu-id="c27de-161">No hello seção de configuração da Citrix GoToMeeting SAML, clique em Configurar SAML do Citrix GoToMeeting tooopen configurar logon na janela.</span><span class="sxs-lookup"><span data-stu-id="c27de-161">On hello Citrix GoToMeeting SAML Configuration section, click Configure Citrix GoToMeeting SAML tooopen Configure sign-on window.</span></span> <span data-ttu-id="c27de-162">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="c27de-162">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

6. <span data-ttu-id="c27de-163">Em uma janela de navegador diferente, faça logon no tooyour [Citrix organização Center](https://account.citrixonline.com/organization/administration/).</span><span class="sxs-lookup"><span data-stu-id="c27de-163">In a different browser window, log in tooyour [Citrix Organization Center](https://account.citrixonline.com/organization/administration/).</span></span>

7. <span data-ttu-id="c27de-164">Clique em Olá **provedor de identidade** guia e, em seguida, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c27de-164">Click hello **Identity Provider** tab, and then perform hello following steps:</span></span>  
   
    <span data-ttu-id="c27de-165">![Instalação do SAML](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "Instalação do SAML")</span><span class="sxs-lookup"><span data-stu-id="c27de-165">![SAML setup](./media/active-directory-saas-citrix-gotomeeting-tutorial/IC6892321.png "SAML setup")</span></span>
   
    <span data-ttu-id="c27de-166">a.</span><span class="sxs-lookup"><span data-stu-id="c27de-166">a.</span></span> <span data-ttu-id="c27de-167">Selecione **Manual**</span><span class="sxs-lookup"><span data-stu-id="c27de-167">Select **Manual**</span></span>

    <span data-ttu-id="c27de-168">b.</span><span class="sxs-lookup"><span data-stu-id="c27de-168">b.</span></span> <span data-ttu-id="c27de-169">Em Olá portal do Azure, Olá **configurar logon único no Citrix GoToMeeting** página de diálogo, Olá cópia **Single Sign-On URL do serviço SAML** valor e, em seguida, cole-o em Olá **na página de entrada URL** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="c27de-169">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **Sign-in page URL** textbox.</span></span> 

    <span data-ttu-id="c27de-170">c.</span><span class="sxs-lookup"><span data-stu-id="c27de-170">c.</span></span> <span data-ttu-id="c27de-171">Em Olá portal do Azure, Olá **configurar logon único no Citrix GoToMeeting** página de diálogo, Olá cópia **URL de logout** valor e, em seguida, cole-o em Olá **URL da página de logout**caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="c27de-171">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **Sign-Out URL** value, and then paste it into hello **Sign-out page URL** textbox.</span></span>

    <span data-ttu-id="c27de-172">d.</span><span class="sxs-lookup"><span data-stu-id="c27de-172">d.</span></span> <span data-ttu-id="c27de-173">Em Olá portal do Azure, Olá **configurar logon único no Citrix GoToMeeting** página de diálogo, Olá cópia **ID da entidade SAML** valor e, em seguida, cole-Olá **ID de entidade do provedor de identidade**  caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="c27de-173">In hello Azure portal, on hello **Configure single sign-on at Citrix GoToMeeting** dialog page, copy hello **SAML Entity ID** value, and then paste it into hello **Identity Provider Entity ID** textbox.</span></span>

    <span data-ttu-id="c27de-174">e.</span><span class="sxs-lookup"><span data-stu-id="c27de-174">e.</span></span> <span data-ttu-id="c27de-175">tooupload seu certificado baixado, clique em **carregar certificado**.</span><span class="sxs-lookup"><span data-stu-id="c27de-175">tooupload your downloaded certificate, click **Upload Certificate**.</span></span>

    <span data-ttu-id="c27de-176">f.</span><span class="sxs-lookup"><span data-stu-id="c27de-176">f.</span></span> <span data-ttu-id="c27de-177">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c27de-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c27de-178">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c27de-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c27de-179">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c27de-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c27de-180">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c27de-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c27de-181">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c27de-181">Creating an Azure AD test user</span></span>
<span data-ttu-id="c27de-182">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c27de-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c27de-184">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c27de-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c27de-185">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c27de-185">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c27de-187">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c27de-187">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c27de-189">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c27de-189">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c27de-191">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c27de-191">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-citrix-gotomeeting-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c27de-193">a.</span><span class="sxs-lookup"><span data-stu-id="c27de-193">a.</span></span> <span data-ttu-id="c27de-194">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c27de-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c27de-195">b.</span><span class="sxs-lookup"><span data-stu-id="c27de-195">b.</span></span> <span data-ttu-id="c27de-196">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c27de-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c27de-197">c.</span><span class="sxs-lookup"><span data-stu-id="c27de-197">c.</span></span> <span data-ttu-id="c27de-198">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c27de-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c27de-199">d.</span><span class="sxs-lookup"><span data-stu-id="c27de-199">d.</span></span> <span data-ttu-id="c27de-200">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c27de-200">Click **Create**.</span></span>
 
### <a name="creating-a-citrix-gotomeeting-test-user"></a><span data-ttu-id="c27de-201">Criando um usuário de teste do Citrix GoToMeeting</span><span class="sxs-lookup"><span data-stu-id="c27de-201">Creating a Citrix GoToMeeting test user</span></span>

<span data-ttu-id="c27de-202">Nesta seção, é criado um usuário chamado Brenda Fernandes no Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="c27de-202">In this section, a user called Britta Simon is created in Citrix GoToMeeting.</span></span> <span data-ttu-id="c27de-203">O Citrix GoToMeeting dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="c27de-203">Citrix GoToMeeting supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="c27de-204">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="c27de-204">There is no action item for you in this section.</span></span> <span data-ttu-id="c27de-205">Se um usuário não existir no Citrix GoToMeeting, um novo é criado quando você tenta tooaccess Citrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="c27de-205">If a user doesn't already exist in Citrix GoToMeeting, a new one is created when you attempt tooaccess Citrix GoToMeeting.</span></span>

>[!Note]
><span data-ttu-id="c27de-206">Se você precisar toocreate um usuário manualmente, entre em contato com [equipe de suporte do Citrix GoToMeeting](https://care.citrixonline.com/gotomeeting)</span><span class="sxs-lookup"><span data-stu-id="c27de-206">If you need toocreate a user manually, Contact [Citrix GoToMeeting support team](https://care.citrixonline.com/gotomeeting)</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c27de-207">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c27de-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c27de-208">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooCitrix GoToMeeting.</span><span class="sxs-lookup"><span data-stu-id="c27de-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCitrix GoToMeeting.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c27de-210">**tooassign tooCitrix Britta Simon GoToMeeting, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c27de-210">**tooassign Britta Simon tooCitrix GoToMeeting, perform hello following steps:**</span></span>

1. <span data-ttu-id="c27de-211">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c27de-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c27de-213">Na lista de aplicativos hello, selecione **Citrix GoToMeeting**.</span><span class="sxs-lookup"><span data-stu-id="c27de-213">In hello applications list, select **Citrix GoToMeeting**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_citrix-gotomeeting_app.png) 

3. <span data-ttu-id="c27de-215">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c27de-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c27de-217">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c27de-217">Click **Add** button.</span></span> <span data-ttu-id="c27de-218">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c27de-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c27de-220">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c27de-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c27de-221">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c27de-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c27de-222">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c27de-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c27de-223">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c27de-223">Testing single sign-on</span></span>

<span data-ttu-id="c27de-224">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c27de-224">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c27de-225">Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="c27de-225">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="c27de-226">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c27de-226">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c27de-227">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c27de-227">Additional resources</span></span>

* [<span data-ttu-id="c27de-228">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c27de-228">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c27de-229">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c27de-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c27de-230">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="c27de-230">Configure User Provisioning</span></span>](active-directory-saas-citrixgotomeeting-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-citrix-gotomeeting-tutorial/tutorial_general_203.png

