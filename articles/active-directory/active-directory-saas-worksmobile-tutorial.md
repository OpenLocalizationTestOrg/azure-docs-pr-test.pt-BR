---
title: "Tutorial: Integração do Azure Active Directory com o WORKS MOBILE | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e móveis funciona."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 80192218a2e99a921834bb53e708d5e4fab413f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="c8b66-103">Tutorial: Integração do Azure Active Directory com o WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="c8b66-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="c8b66-104">Neste tutorial, você aprenderá como funciona o toointegrate móvel com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c8b66-104">In this tutorial, you learn how toointegrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c8b66-105">Integrando móveis funciona com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8b66-105">Integrating WORKS MOBILE with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c8b66-106">Você pode controlar no AD do Azure que tenha acesso tooWORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="c8b66-106">You can control in Azure AD who has access tooWORKS MOBILE</span></span>
- <span data-ttu-id="c8b66-107">Você pode habilitar seus usuários tooautomatically get conectado tooWORKS MOBILE (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8b66-107">You can enable your users tooautomatically get signed-on tooWORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c8b66-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c8b66-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c8b66-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c8b66-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8b66-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c8b66-110">Prerequisites</span></span>

<span data-ttu-id="c8b66-111">tooconfigure integração do AD do Azure com o MOBILE funciona, é necessário Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8b66-111">tooconfigure Azure AD integration with WORKS MOBILE, you need hello following items:</span></span>

- <span data-ttu-id="c8b66-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8b66-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c8b66-113">Uma assinatura do WORKS MOBILE com logon único habilitado</span><span class="sxs-lookup"><span data-stu-id="c8b66-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c8b66-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c8b66-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c8b66-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c8b66-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c8b66-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c8b66-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c8b66-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c8b66-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c8b66-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c8b66-118">Scenario description</span></span>
<span data-ttu-id="c8b66-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c8b66-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c8b66-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c8b66-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c8b66-121">Adicionando MOBILE funciona da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c8b66-121">Adding WORKS MOBILE from hello gallery</span></span>
2. <span data-ttu-id="c8b66-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8b66-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-hello-gallery"></a><span data-ttu-id="c8b66-123">Adicionando MOBILE funciona da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c8b66-123">Adding WORKS MOBILE from hello gallery</span></span>
<span data-ttu-id="c8b66-124">integração de Olá tooconfigure do MOBILE funciona no AD do Azure, você precisa tooadd funciona móvel da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c8b66-124">tooconfigure hello integration of WORKS MOBILE into Azure AD, you need tooadd WORKS MOBILE from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c8b66-125">**tooadd móvel funciona da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c8b66-125">**tooadd WORKS MOBILE from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8b66-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c8b66-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c8b66-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c8b66-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c8b66-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8b66-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c8b66-133">Na caixa de pesquisa hello, digite **funciona MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-133">In hello search box, type **WORKS MOBILE**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="c8b66-135">No painel de resultados de saudação, selecione **funciona MOBILE**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c8b66-135">In hello results panel, select **WORKS MOBILE**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c8b66-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8b66-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c8b66-138">Nesta seção, você configurará e testará o logon único do Azure AD com o WORKS MOBILE, com base em uma usuária de teste chamada “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c8b66-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c8b66-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no MOBILE funciona é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8b66-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in WORKS MOBILE is tooa user in Azure AD.</span></span> <span data-ttu-id="c8b66-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no WORKS MOBILE precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c8b66-140">In other words, a link relationship between an Azure AD user and hello related user in WORKS MOBILE needs toobe established.</span></span>

<span data-ttu-id="c8b66-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no MOBILE funciona.</span><span class="sxs-lookup"><span data-stu-id="c8b66-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="c8b66-142">tooconfigure e teste de logon único do AD do Azure com o MOBILE funciona, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8b66-142">tooconfigure and test Azure AD single sign-on with WORKS MOBILE, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c8b66-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c8b66-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c8b66-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c8b66-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c8b66-145">**[Criar um usuário de teste funciona MOBILE](#creating-a-works-mobile-test-user)**  -toohave um equivalente do Britta Simon no WORKS MOBILE que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c8b66-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - toohave a counterpart of Britta Simon in WORKS MOBILE that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c8b66-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c8b66-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c8b66-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c8b66-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c8b66-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8b66-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c8b66-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo móvel funciona.</span><span class="sxs-lookup"><span data-stu-id="c8b66-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="c8b66-150">**tooconfigure AD do Azure-logon único com o MOBILE funciona, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c8b66-150">**tooconfigure Azure AD single sign-on with WORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8b66-151">Em Olá portal do Azure, Olá **funciona MOBILE** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-151">In hello Azure portal, on hello **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c8b66-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c8b66-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="c8b66-155">Em Olá **funciona MOBILE domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8b66-155">On hello **WORKS MOBILE Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="c8b66-157">a.</span><span class="sxs-lookup"><span data-stu-id="c8b66-157">a.</span></span> <span data-ttu-id="c8b66-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="c8b66-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="c8b66-159">b.</span><span class="sxs-lookup"><span data-stu-id="c8b66-159">b.</span></span> <span data-ttu-id="c8b66-160">Em Olá **identificador** texto, o valor do tipo hello como`worksmobile.com`</span><span class="sxs-lookup"><span data-stu-id="c8b66-160">In hello **Identifier** textbox, type hello value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c8b66-161">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="c8b66-161">This value is not real.</span></span> <span data-ttu-id="c8b66-162">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="c8b66-162">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="c8b66-163">Entre em contato com [a equipe de suporte de cliente móvel funciona](mailto:dl_ssoinfo@worksmobile.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="c8b66-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="c8b66-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Raw)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c8b66-164">On hello **SAML Signing Certificate** section, click **Certificate(Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="c8b66-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c8b66-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c8b66-168">Em Olá **funciona MOBILE configuração** seção, clique em **configurar funciona MOBILE** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="c8b66-168">On hello **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c8b66-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="c8b66-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="c8b66-171">tooget SSO configurado para o seu aplicativo, entre em contato com [a equipe de suporte móvel funciona](mailto:dl_ssoinfo@worksmobile.com) e fornecê-los com hello informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8b66-171">tooget SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with hello following information:</span></span> 

    <span data-ttu-id="c8b66-172">• Olá baixado **arquivo de certificado**</span><span class="sxs-lookup"><span data-stu-id="c8b66-172">• hello downloaded **Certificate file**</span></span>

    <span data-ttu-id="c8b66-173">• Olá **Single Sign-On URL do serviço SAML**</span><span class="sxs-lookup"><span data-stu-id="c8b66-173">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="c8b66-174">• Olá **ID de entidade de SAML**</span><span class="sxs-lookup"><span data-stu-id="c8b66-174">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="c8b66-175">• Olá **URL de logout**</span><span class="sxs-lookup"><span data-stu-id="c8b66-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="c8b66-176">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c8b66-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c8b66-177">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c8b66-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c8b66-178">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c8b66-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c8b66-179">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8b66-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="c8b66-180">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c8b66-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c8b66-182">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c8b66-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8b66-183">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c8b66-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c8b66-185">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c8b66-187">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8b66-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c8b66-189">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c8b66-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c8b66-191">a.</span><span class="sxs-lookup"><span data-stu-id="c8b66-191">a.</span></span> <span data-ttu-id="c8b66-192">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c8b66-193">b.</span><span class="sxs-lookup"><span data-stu-id="c8b66-193">b.</span></span> <span data-ttu-id="c8b66-194">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c8b66-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c8b66-195">c.</span><span class="sxs-lookup"><span data-stu-id="c8b66-195">c.</span></span> <span data-ttu-id="c8b66-196">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c8b66-197">d.</span><span class="sxs-lookup"><span data-stu-id="c8b66-197">d.</span></span> <span data-ttu-id="c8b66-198">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="c8b66-199">Criar um usuário de teste do WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="c8b66-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="c8b66-200">Nesta seção, você criará uma usuária chamada Britta Simon no WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="c8b66-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="c8b66-201">Trabalhe com [a equipe de suporte móvel funciona](mailto:dl_ssoinfo@worksmobile.com) tooadd usuários Olá plataforma Olá funciona.</span><span class="sxs-lookup"><span data-stu-id="c8b66-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) tooadd hello users in hello WORKS MOBILE platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c8b66-202">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c8b66-202">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c8b66-203">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooWORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="c8b66-203">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWORKS MOBILE.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c8b66-205">**tooassign Britta Simon tooWORKS móveis, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c8b66-205">**tooassign Britta Simon tooWORKS MOBILE, perform hello following steps:**</span></span>

1. <span data-ttu-id="c8b66-206">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-206">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c8b66-208">Na lista de aplicativos hello, selecione **funciona MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-208">In hello applications list, select **WORKS MOBILE**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="c8b66-210">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-210">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c8b66-212">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c8b66-212">Click **Add** button.</span></span> <span data-ttu-id="c8b66-213">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8b66-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c8b66-215">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8b66-215">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c8b66-216">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8b66-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c8b66-217">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c8b66-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c8b66-218">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c8b66-218">Testing single sign-on</span></span>

<span data-ttu-id="c8b66-219">Nesta seção, você deve testar sua configuração de SSO do AD do Azure usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c8b66-219">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="c8b66-220">Quando você clica em bloco funciona MOBILE Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour funciona MOBILE application.</span><span class="sxs-lookup"><span data-stu-id="c8b66-220">When you click hello WORKS MOBILE tile in hello Access Panel, you should get automatically signed-on tooyour WORKS MOBILE application.</span></span>
<span data-ttu-id="c8b66-221">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8b66-221">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c8b66-222">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c8b66-222">Additional resources</span></span>

* [<span data-ttu-id="c8b66-223">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c8b66-223">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c8b66-224">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c8b66-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

