---
title: "Tutorial: integração do Azure Active Directory ao eDigitalResearch | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e eDigitalResearch."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: c6b66ea0-16ba-45b4-b550-e81c56262b1f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 6dd3cafb25ef8ede3a4c16902ed8da69cb7b715f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-edigitalresearch"></a><span data-ttu-id="22635-103">Tutorial: integração do Azure Active Directory ao eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="22635-103">Tutorial: Azure Active Directory integration with eDigitalResearch</span></span>

<span data-ttu-id="22635-104">Neste tutorial, você aprenderá como eDigitalResearch toointegrate com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="22635-104">In this tutorial, you learn how toointegrate eDigitalResearch with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="22635-105">Integrando eDigitalResearch com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="22635-105">Integrating eDigitalResearch with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="22635-106">Você pode controlar no AD do Azure que tenha acesso tooeDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="22635-106">You can control in Azure AD who has access tooeDigitalResearch.</span></span>
- <span data-ttu-id="22635-107">Você pode habilitar seu usuários tooautomatically get conectado tooeDigitalResearch (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="22635-107">You can enable your users tooautomatically get signed-on tooeDigitalResearch (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="22635-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="22635-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="22635-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="22635-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22635-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="22635-110">Prerequisites</span></span>

<span data-ttu-id="22635-111">tooconfigure integração do AD do Azure com eDigitalResearch, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="22635-111">tooconfigure Azure AD integration with eDigitalResearch, you need hello following items:</span></span>

- <span data-ttu-id="22635-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="22635-112">An Azure AD subscription</span></span>
- <span data-ttu-id="22635-113">Uma assinatura do eDigitalResearch habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="22635-113">A eDigitalResearch single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="22635-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="22635-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="22635-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="22635-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="22635-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="22635-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="22635-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="22635-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="22635-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="22635-118">Scenario description</span></span>
<span data-ttu-id="22635-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="22635-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="22635-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="22635-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="22635-121">Adicionando eDigitalResearch da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="22635-121">Adding eDigitalResearch from hello gallery</span></span>
2. <span data-ttu-id="22635-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="22635-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-edigitalresearch-from-hello-gallery"></a><span data-ttu-id="22635-123">Adicionando eDigitalResearch da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="22635-123">Adding eDigitalResearch from hello gallery</span></span>
<span data-ttu-id="22635-124">integração de saudação tooconfigure de eDigitalResearch no AD do Azure, você precisa eDigitalResearch tooadd da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="22635-124">tooconfigure hello integration of eDigitalResearch into Azure AD, you need tooadd eDigitalResearch from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="22635-125">**eDigitalResearch tooadd da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="22635-125">**tooadd eDigitalResearch from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="22635-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="22635-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="22635-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="22635-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="22635-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="22635-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="22635-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="22635-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="22635-133">Na caixa de pesquisa hello, digite **eDigitalResearch**, selecione **eDigitalResearch** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="22635-133">In hello search box, type **eDigitalResearch**, select **eDigitalResearch** from result panel then click **Add** button tooadd hello application.</span></span>

    ![eDigitalResearch na lista de resultados de saudação](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="22635-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="22635-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="22635-136">Nesta seção, você configurará e testará o logon único do Azure AD com o eDigitalResearch, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="22635-136">In this section, you configure and test Azure AD single sign-on with eDigitalResearch based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="22635-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em eDigitalResearch é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="22635-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eDigitalResearch is tooa user in Azure AD.</span></span> <span data-ttu-id="22635-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em eDigitalResearch precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="22635-138">In other words, a link relationship between an Azure AD user and hello related user in eDigitalResearch needs toobe established.</span></span>

<span data-ttu-id="22635-139">EDigitalResearch, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="22635-139">In eDigitalResearch, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="22635-140">tooconfigure e teste de logon único do AD do Azure com eDigitalResearch, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="22635-140">tooconfigure and test Azure AD single sign-on with eDigitalResearch, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="22635-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="22635-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="22635-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="22635-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="22635-143">**[Criar um usuário de teste eDigitalResearch](#create-a-edigitalresearch-test-user)**  -toohave um equivalente do Britta Simon em eDigitalResearch é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="22635-143">**[Create a eDigitalResearch test user](#create-a-edigitalresearch-test-user)** - toohave a counterpart of Britta Simon in eDigitalResearch that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="22635-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="22635-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="22635-145">**[Testar o logon único](#test-single-sign-on)**  tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="22635-145">**[Test single sign-on](#test-single-sign-on)**  tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="22635-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="22635-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="22635-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="22635-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eDigitalResearch application.</span></span>

<span data-ttu-id="22635-148">**tooconfigure AD do Azure-logon único com eDigitalResearch, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="22635-148">**tooconfigure Azure AD single sign-on with eDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="22635-149">Em Olá portal do Azure, Olá **eDigitalResearch** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="22635-149">In hello Azure portal, on hello **eDigitalResearch** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="22635-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="22635-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_samlbase.png)

3. <span data-ttu-id="22635-153">Em Olá **eDigitalResearch domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="22635-153">On hello **eDigitalResearch Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_url.png)

    <span data-ttu-id="22635-155">a.</span><span class="sxs-lookup"><span data-stu-id="22635-155">a.</span></span> <span data-ttu-id="22635-156">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company-name>.edigitalresearch.com`</span><span class="sxs-lookup"><span data-stu-id="22635-156">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com`</span></span>

    <span data-ttu-id="22635-157">b.</span><span class="sxs-lookup"><span data-stu-id="22635-157">b.</span></span> <span data-ttu-id="22635-158">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<company-name>.edigitalresearch.com/login/consume`</span><span class="sxs-lookup"><span data-stu-id="22635-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company-name>.edigitalresearch.com/login/consume`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="22635-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="22635-159">These values are not real.</span></span> <span data-ttu-id="22635-160">Atualize esses valores com URL de resposta e o identificador de real de saudação.</span><span class="sxs-lookup"><span data-stu-id="22635-160">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="22635-161">Entre em contato com [eDigitalResearch a equipe de suporte](http://www.maruedr.com/contact) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="22635-161">Contact [eDigitalResearch support team](http://www.maruedr.com/contact) tooget these values.</span></span>
 


4. <span data-ttu-id="22635-162">Em Olá **o certificado de autenticação SAML** seção, clique em **Base(64) certificado** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="22635-162">On hello **SAML Signing Certificate** section, click **Certificate Base(64)** and then save hello certificate file on your computer.</span></span>

    <span data-ttu-id="22635-163">!</span><span class="sxs-lookup"><span data-stu-id="22635-163">!</span></span>![link de download de certificado Olá](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_certificate.png) 

5. <span data-ttu-id="22635-165">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="22635-165">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="22635-167">Em Olá **eDigitalResearch configuração** seção, clique em **configurar eDigitalResearch** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="22635-167">On hello **eDigitalResearch Configuration** section, click **Configure eDigitalResearch** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="22635-168">Saudação de cópia **URL de logout, ID da entidade SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="22635-168">Copy hello **Sign-Out URL, SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configuração do eDigitalResearch](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_configure.png) 

7. <span data-ttu-id="22635-170">tooconfigure logon único no **eDigitalResearch** lado, você precisa toosend Olá baixado **arquivo de certificado (Base64)**, **ID da entidade SAML**, e  **URL de saída** muito[a equipe de suporte eDigitalResearch](http://www.maruedr.com/contact).</span><span class="sxs-lookup"><span data-stu-id="22635-170">tooconfigure single sign-on on **eDigitalResearch** side, you need toosend hello downloaded **Certificate (Base64) File**, **SAML Entity ID**, and **Sign-Out URL** too[eDigitalResearch support team](http://www.maruedr.com/contact).</span></span> <span data-ttu-id="22635-171">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="22635-171">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="22635-172">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="22635-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="22635-173">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="22635-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="22635-174">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="22635-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="22635-175">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="22635-175">Create an Azure AD test user</span></span>

<span data-ttu-id="22635-176">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="22635-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="22635-178">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="22635-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="22635-179">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="22635-179">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="22635-181">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="22635-181">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="22635-183">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="22635-183">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="22635-185">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="22635-185">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-edigitalresearch-tutorial/create_aaduser_04.png)

    <span data-ttu-id="22635-187">a.</span><span class="sxs-lookup"><span data-stu-id="22635-187">a.</span></span> <span data-ttu-id="22635-188">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="22635-188">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="22635-189">b.</span><span class="sxs-lookup"><span data-stu-id="22635-189">b.</span></span> <span data-ttu-id="22635-190">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="22635-190">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="22635-191">c.</span><span class="sxs-lookup"><span data-stu-id="22635-191">c.</span></span> <span data-ttu-id="22635-192">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="22635-192">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="22635-193">d.</span><span class="sxs-lookup"><span data-stu-id="22635-193">d.</span></span> <span data-ttu-id="22635-194">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="22635-194">Click **Create**.</span></span>
  
### <a name="create-a-edigitalresearch-test-user"></a><span data-ttu-id="22635-195">Criar um usuário de teste eDigitalResearch</span><span class="sxs-lookup"><span data-stu-id="22635-195">Create a eDigitalResearch test user</span></span>

<span data-ttu-id="22635-196">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no eDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="22635-196">hello objective of this section is toocreate a user called Britta Simon in eDigitalResearch.</span></span> 

<span data-ttu-id="22635-197">Trabalhar com hello [eDigitalResearch a equipe de suporte](http://www.maruedr.com/contact) tooget usuários criados.</span><span class="sxs-lookup"><span data-stu-id="22635-197">Work with hello [eDigitalResearch support team](http://www.maruedr.com/contact) tooget users created.</span></span>       
    
 > [!NOTE]
 > <span data-ttu-id="22635-198">proprietário de conta do Active Directory do Azure Olá recebe um email e segue um link tooconfirm sua conta antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="22635-198">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="22635-199">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="22635-199">Assign hello Azure AD test user</span></span>

<span data-ttu-id="22635-200">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooeDigitalResearch.</span><span class="sxs-lookup"><span data-stu-id="22635-200">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeDigitalResearch.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="22635-202">**tooassign Britta Simon tooeDigitalResearch, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="22635-202">**tooassign Britta Simon tooeDigitalResearch, perform hello following steps:**</span></span>

1. <span data-ttu-id="22635-203">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="22635-203">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="22635-205">Na lista de aplicativos hello, selecione **eDigitalResearch**.</span><span class="sxs-lookup"><span data-stu-id="22635-205">In hello applications list, select **eDigitalResearch**.</span></span>

    ![Olá eDigitalResearch link na lista de aplicativos Olá](./media/active-directory-saas-edigitalresearch-tutorial/tutorial_edigitalresearch_app.png)  

3. <span data-ttu-id="22635-207">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="22635-207">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="22635-209">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="22635-209">Click **Add** button.</span></span> <span data-ttu-id="22635-210">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="22635-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="22635-212">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="22635-212">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="22635-213">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="22635-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="22635-214">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="22635-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="22635-215">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="22635-215">Test single sign-on</span></span>

<span data-ttu-id="22635-216">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="22635-216">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="22635-217">Quando você clica em bloco eDigitalResearch Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour eDigitalResearch aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22635-217">When you click hello eDigitalResearch tile in hello Access Panel, you should get automatically signed-on tooyour eDigitalResearch application.</span></span>
<span data-ttu-id="22635-218">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="22635-218">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="22635-219">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="22635-219">Additional resources</span></span>

* [<span data-ttu-id="22635-220">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="22635-220">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="22635-221">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="22635-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-edigitalresearch-tutorial/tutorial_general_203.png

