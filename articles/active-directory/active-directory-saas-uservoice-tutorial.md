---
title: "Tutorial: Integração do Azure Active Directory com o UserVoice | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e UserVoice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 684a405b-8932-46f6-b43a-4d97a42b6b87
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: 9eade8435ae6c6a3821bbbec9ab7c27ed7ad91ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-uservoice"></a><span data-ttu-id="9a93a-103">Tutorial: Integração do Azure Active Directory com o UserVoice</span><span class="sxs-lookup"><span data-stu-id="9a93a-103">Tutorial: Azure Active Directory integration with UserVoice</span></span>

<span data-ttu-id="9a93a-104">Neste tutorial, você aprenderá como toointegrate UserVoice com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="9a93a-104">In this tutorial, you learn how toointegrate UserVoice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9a93a-105">Integrando o UserVoice com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a93a-105">Integrating UserVoice with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9a93a-106">Você pode controlar no AD do Azure que tenha acesso tooUserVoice.</span><span class="sxs-lookup"><span data-stu-id="9a93a-106">You can control in Azure AD who has access tooUserVoice.</span></span>
- <span data-ttu-id="9a93a-107">Você pode habilitar seu usuários tooautomatically get conectado tooUserVoice (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a93a-107">You can enable your users tooautomatically get signed-on tooUserVoice (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9a93a-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a93a-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="9a93a-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9a93a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a93a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9a93a-110">Prerequisites</span></span>

<span data-ttu-id="9a93a-111">tooconfigure integração do AD do Azure com o UserVoice, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a93a-111">tooconfigure Azure AD integration with UserVoice, you need hello following items:</span></span>

- <span data-ttu-id="9a93a-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9a93a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9a93a-113">Uma assinatura do UserVoice com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="9a93a-113">A UserVoice single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9a93a-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9a93a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9a93a-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9a93a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9a93a-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9a93a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9a93a-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9a93a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9a93a-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9a93a-118">Scenario description</span></span>
<span data-ttu-id="9a93a-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9a93a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9a93a-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="9a93a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9a93a-121">Adicionando UserVoice da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9a93a-121">Adding UserVoice from hello gallery</span></span>
2. <span data-ttu-id="9a93a-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9a93a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-uservoice-from-hello-gallery"></a><span data-ttu-id="9a93a-123">Adicionando UserVoice da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9a93a-123">Adding UserVoice from hello gallery</span></span>
<span data-ttu-id="9a93a-124">integração de saudação tooconfigure do UserVoice no AD do Azure, você precisa tooadd UserVoice da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9a93a-124">tooconfigure hello integration of UserVoice into Azure AD, you need tooadd UserVoice from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9a93a-125">**tooadd UserVoice da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9a93a-125">**tooadd UserVoice from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a93a-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9a93a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="9a93a-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9a93a-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="9a93a-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9a93a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="9a93a-133">Na caixa de pesquisa hello, digite **UserVoice**, selecione **UserVoice** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9a93a-133">In hello search box, type **UserVoice**, select **UserVoice** from result panel then click **Add** button tooadd hello application.</span></span>

    ![UserVoice na lista de resultados de saudação](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9a93a-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a93a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9a93a-136">Nesta seção, você configurará e testará o logon único do Azure AD com o UserVoice, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="9a93a-136">In this section, you configure and test Azure AD single sign-on with UserVoice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9a93a-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no UserVoice é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a93a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UserVoice is tooa user in Azure AD.</span></span> <span data-ttu-id="9a93a-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no UserVoice precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="9a93a-138">In other words, a link relationship between an Azure AD user and hello related user in UserVoice needs toobe established.</span></span>

<span data-ttu-id="9a93a-139">No UserVoice, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a93a-139">In UserVoice, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9a93a-140">tooconfigure e teste de logon único do AD do Azure com o UserVoice, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a93a-140">tooconfigure and test Azure AD single sign-on with UserVoice, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9a93a-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9a93a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9a93a-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a93a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9a93a-143">**[Criar um usuário de teste do UserVoice](#create-a-uservoice-test-user)**  -toohave um equivalente do Britta Simon no UserVoice é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="9a93a-143">**[Create a UserVoice test user](#create-a-uservoice-test-user)** - toohave a counterpart of Britta Simon in UserVoice that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9a93a-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="9a93a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9a93a-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="9a93a-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9a93a-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a93a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9a93a-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do UserVoice.</span><span class="sxs-lookup"><span data-stu-id="9a93a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UserVoice application.</span></span>

<span data-ttu-id="9a93a-148">**tooconfigure AD do Azure-logon único com o UserVoice, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9a93a-148">**tooconfigure Azure AD single sign-on with UserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a93a-149">Em Olá portal do Azure, Olá **UserVoice** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-149">In hello Azure portal, on hello **UserVoice** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="9a93a-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="9a93a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_samlbase.png)

3. <span data-ttu-id="9a93a-153">Em Olá **UserVoice domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a93a-153">On hello **UserVoice Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de URLs e Domínio do UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_url.png)

    <span data-ttu-id="9a93a-155">a.</span><span class="sxs-lookup"><span data-stu-id="9a93a-155">a.</span></span> <span data-ttu-id="9a93a-156">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="9a93a-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    <span data-ttu-id="9a93a-157">b.</span><span class="sxs-lookup"><span data-stu-id="9a93a-157">b.</span></span> <span data-ttu-id="9a93a-158">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.UserVoice.com`</span><span class="sxs-lookup"><span data-stu-id="9a93a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenantname>.UserVoice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9a93a-159">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="9a93a-159">These values are not real.</span></span> <span data-ttu-id="9a93a-160">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="9a93a-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9a93a-161">Entre em contato com [equipe de suporte do cliente do UserVoice](https://www.uservoice.com/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="9a93a-161">Contact [UserVoice Client support team](https://www.uservoice.com/) tooget these values.</span></span>

4. <span data-ttu-id="9a93a-162">Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** o valor de certificado.</span><span class="sxs-lookup"><span data-stu-id="9a93a-162">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_certificate.png) 

5. <span data-ttu-id="9a93a-164">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9a93a-164">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-uservoice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9a93a-166">Em Olá **UserVoice configuração** seção, clique em **configurar UserVoice** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="9a93a-166">On hello **UserVoice Configuration** section, click **Configure UserVoice** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9a93a-167">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="9a93a-167">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do UserVoice](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_configure.png) 

7. <span data-ttu-id="9a93a-169">Em uma janela de navegador web diferente, faça logon no site da empresa tooyour UserVoice como um administrador.</span><span class="sxs-lookup"><span data-stu-id="9a93a-169">In a different web browser window, log in tooyour UserVoice company site as an administrator.</span></span>

8. <span data-ttu-id="9a93a-170">Na barra de ferramentas de saudação na parte superior do hello, clique em **configurações**e, em seguida, selecione **portal da Web** menu hello.</span><span class="sxs-lookup"><span data-stu-id="9a93a-170">In hello toolbar on hello top, click **Settings**, and then select **Web portal** from hello menu.</span></span>
   
    <span data-ttu-id="9a93a-171">![Seção Configurações no lado do aplicativo](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="9a93a-171">![Settings Section On App Side](./media/active-directory-saas-uservoice-tutorial/ic777519.png "Settings")</span></span>

9. <span data-ttu-id="9a93a-172">Em Olá **portal da Web** guia Olá **autenticação de usuário** seção, clique em **editar** tooopen Olá **Editar autenticação de usuário** caixa de diálogo página.</span><span class="sxs-lookup"><span data-stu-id="9a93a-172">On hello **Web portal** tab, in hello **User authentication** section, click **Edit** tooopen hello **Edit User Authentication** dialog page.</span></span>
   
    <span data-ttu-id="9a93a-173">![Guia Portal da Web](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Portal da Web")</span><span class="sxs-lookup"><span data-stu-id="9a93a-173">![Web portal Tab](./media/active-directory-saas-uservoice-tutorial/ic777520.png "Web portal")</span></span>

10. <span data-ttu-id="9a93a-174">Em Olá **Editar autenticação de usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a93a-174">On hello **Edit User Authentication** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="9a93a-175">![Editar autenticação de usuário](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Editar autenticação de usuário")</span><span class="sxs-lookup"><span data-stu-id="9a93a-175">![Edit user authentication](./media/active-directory-saas-uservoice-tutorial/ic777521.png "Edit user authentication")</span></span>
   
    <span data-ttu-id="9a93a-176">a.</span><span class="sxs-lookup"><span data-stu-id="9a93a-176">a.</span></span> <span data-ttu-id="9a93a-177">Clique em **SSO (Logon Único)**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-177">Click **Single Sign-On (SSO)**.</span></span>
 
    <span data-ttu-id="9a93a-178">b.</span><span class="sxs-lookup"><span data-stu-id="9a93a-178">b.</span></span> <span data-ttu-id="9a93a-179">Saudação de colar **Single Sign-On URL do serviço SAML** valor que você copiou de saudação portal do Azure em hello **entrar remoto SSO** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="9a93a-179">Paste hello **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-In** textbox.</span></span>

    <span data-ttu-id="9a93a-180">c.</span><span class="sxs-lookup"><span data-stu-id="9a93a-180">c.</span></span> <span data-ttu-id="9a93a-181">Saudação de colar **URL de logout** valor que você copiou de saudação portal do Azure em hello **caixa de texto de saída remota de SSO**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-181">Paste hello **Sign-Out URL** value, which you have copied from hello Azure portal into hello **SSO Remote Sign-Out textbox**.</span></span>
 
    <span data-ttu-id="9a93a-182">d.</span><span class="sxs-lookup"><span data-stu-id="9a93a-182">d.</span></span> <span data-ttu-id="9a93a-183">Saudação de colar **impressão digital** valor, que você copiou do portal do Azure para o **impressão digital de certificado SHA1 atual** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="9a93a-183">Paste hello **Thumbprint** value , which you have copied from Azure portal  into the **Current certificate SHA1 fingerprint** textbox.</span></span>
    
    <span data-ttu-id="9a93a-184">e.</span><span class="sxs-lookup"><span data-stu-id="9a93a-184">e.</span></span> <span data-ttu-id="9a93a-185">Clique em **Salvar Configurações de Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-185">Click **Save authentication settings**.</span></span>

> [!TIP]
> <span data-ttu-id="9a93a-186">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="9a93a-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9a93a-187">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="9a93a-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9a93a-188">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9a93a-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9a93a-189">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9a93a-189">Create an Azure AD test user</span></span>

<span data-ttu-id="9a93a-190">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a93a-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="9a93a-192">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9a93a-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a93a-193">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="9a93a-193">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-uservoice-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9a93a-195">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-195">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-uservoice-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9a93a-197">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9a93a-197">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-uservoice-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9a93a-199">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a93a-199">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-uservoice-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9a93a-201">a.</span><span class="sxs-lookup"><span data-stu-id="9a93a-201">a.</span></span> <span data-ttu-id="9a93a-202">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-202">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9a93a-203">b.</span><span class="sxs-lookup"><span data-stu-id="9a93a-203">b.</span></span> <span data-ttu-id="9a93a-204">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9a93a-204">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="9a93a-205">c.</span><span class="sxs-lookup"><span data-stu-id="9a93a-205">c.</span></span> <span data-ttu-id="9a93a-206">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="9a93a-206">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="9a93a-207">d.</span><span class="sxs-lookup"><span data-stu-id="9a93a-207">d.</span></span> <span data-ttu-id="9a93a-208">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-208">Click **Create**.</span></span>
 
### <a name="create-a-uservoice-test-user"></a><span data-ttu-id="9a93a-209">Criar um usuário de teste do UserVoice</span><span class="sxs-lookup"><span data-stu-id="9a93a-209">Create a UserVoice test user</span></span>

<span data-ttu-id="9a93a-210">tooenable AD do Azure usuários toolog em tooUserVoice, eles devem ser provisionados no UserVoice.</span><span class="sxs-lookup"><span data-stu-id="9a93a-210">tooenable Azure AD users toolog in tooUserVoice, they must be provisioned into UserVoice.</span></span> <span data-ttu-id="9a93a-211">No caso de saudação do UserVoice, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="9a93a-211">In hello case of UserVoice, provisioning is a manual task.</span></span>

### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="9a93a-212">tooprovision uma conta de usuário, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a93a-212">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="9a93a-213">Faça logon no tooyour **UserVoice** locatário.</span><span class="sxs-lookup"><span data-stu-id="9a93a-213">Log in tooyour **UserVoice** tenant.</span></span>

2. <span data-ttu-id="9a93a-214">Vá muito**configurações**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-214">Go too**Settings**.</span></span>
   
    <span data-ttu-id="9a93a-215">![Configurações](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="9a93a-215">![Settings](./media/active-directory-saas-uservoice-tutorial/ic777811.png "Settings")</span></span>

3. <span data-ttu-id="9a93a-216">Clique em **Geral**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-216">Click **General**.</span></span>

4. <span data-ttu-id="9a93a-217">Clique em **Agentes e permissões**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-217">Click **Agents and permissions**.</span></span>
   
    <span data-ttu-id="9a93a-218">![Agentes e permissões](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agentes e permissões")</span><span class="sxs-lookup"><span data-stu-id="9a93a-218">![Agents and permissions](./media/active-directory-saas-uservoice-tutorial/ic777812.png "Agents and permissions")</span></span>

5. <span data-ttu-id="9a93a-219">Clique em **Adicionar administradores**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-219">Click **Add admins**.</span></span>
   
    <span data-ttu-id="9a93a-220">![Adicionar administradores](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Adicionar administradores")</span><span class="sxs-lookup"><span data-stu-id="9a93a-220">![Add admins](./media/active-directory-saas-uservoice-tutorial/ic777813.png "Add admins")</span></span>

6. <span data-ttu-id="9a93a-221">Em Olá **convidar administradores** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9a93a-221">On hello **Invite admins** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="9a93a-222">![Convidar administradores](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Convidar administradores")</span><span class="sxs-lookup"><span data-stu-id="9a93a-222">![Invite admins](./media/active-directory-saas-uservoice-tutorial/ic777814.png "Invite admins")</span></span>
   
    <span data-ttu-id="9a93a-223">a.</span><span class="sxs-lookup"><span data-stu-id="9a93a-223">a.</span></span> <span data-ttu-id="9a93a-224">Na caixa de texto de Emails Olá, digite o endereço de email de saudação da conta de Olá você deseja tooprovision e, em seguida, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-224">In hello Emails textbox, type hello email address of hello account you want tooprovision, and then click **Add**.</span></span>
   
    <span data-ttu-id="9a93a-225">b.</span><span class="sxs-lookup"><span data-stu-id="9a93a-225">b.</span></span> <span data-ttu-id="9a93a-226">Clique em **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-226">Click **Invite**.</span></span>

> [!NOTE]
> <span data-ttu-id="9a93a-227">Você pode usar qualquer ferramenta de criação outros UserVoice usuário conta ou APIs fornecidas pelo UserVoice tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="9a93a-227">You can use any other UserVoice user account creation tools or APIs provided by UserVoice tooprovision AAD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9a93a-228">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9a93a-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9a93a-229">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooUserVoice.</span><span class="sxs-lookup"><span data-stu-id="9a93a-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUserVoice.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="9a93a-231">**tooassign Britta Simon tooUserVoice, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9a93a-231">**tooassign Britta Simon tooUserVoice, perform hello following steps:**</span></span>

1. <span data-ttu-id="9a93a-232">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9a93a-234">Na lista de aplicativos hello, selecione **UserVoice**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-234">In hello applications list, select **UserVoice**.</span></span>

    ![link do UserVoice Olá na lista de aplicativos Olá](./media/active-directory-saas-uservoice-tutorial/tutorial_uservoice_app.png)  

3. <span data-ttu-id="9a93a-236">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="9a93a-238">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9a93a-238">Click **Add** button.</span></span> <span data-ttu-id="9a93a-239">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9a93a-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="9a93a-241">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a93a-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9a93a-242">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9a93a-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9a93a-243">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9a93a-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9a93a-244">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="9a93a-244">Test single sign-on</span></span>

<span data-ttu-id="9a93a-245">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="9a93a-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9a93a-246">Quando você clica em bloco UserVoice Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour UserVoice aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9a93a-246">When you click hello UserVoice tile in hello Access Panel, you should get automatically signed-on tooyour UserVoice application.</span></span>
<span data-ttu-id="9a93a-247">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9a93a-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9a93a-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9a93a-248">Additional resources</span></span>

* [<span data-ttu-id="9a93a-249">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9a93a-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9a93a-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9a93a-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-uservoice-tutorial/tutorial_general_203.png

