---
title: "Tutorial: integração do Azure Active Directory ao Origami | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Origami."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a28bb0ba-b564-46ba-accc-e587699295d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: a45f2d2b8d2271cf0fc58cb8fad92f007cb5e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-origami"></a><span data-ttu-id="668b0-103">Tutorial: Integração do Azure Active Directory ao Origami</span><span class="sxs-lookup"><span data-stu-id="668b0-103">Tutorial: Azure Active Directory integration with Origami</span></span>

<span data-ttu-id="668b0-104">Neste tutorial, você aprenderá como toointegrate Origami com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="668b0-104">In this tutorial, you learn how toointegrate Origami with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="668b0-105">Integrando Origami AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="668b0-105">Integrating Origami with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="668b0-106">Você pode controlar no AD do Azure que tenha acesso tooOrigami</span><span class="sxs-lookup"><span data-stu-id="668b0-106">You can control in Azure AD who has access tooOrigami</span></span>
- <span data-ttu-id="668b0-107">Você pode habilitar seu usuários tooautomatically get conectado tooOrigami (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="668b0-107">You can enable your users tooautomatically get signed-on tooOrigami (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="668b0-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="668b0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="668b0-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="668b0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="668b0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="668b0-110">Prerequisites</span></span>

<span data-ttu-id="668b0-111">tooconfigure integração do AD do Azure com Origami, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="668b0-111">tooconfigure Azure AD integration with Origami, you need hello following items:</span></span>

- <span data-ttu-id="668b0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="668b0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="668b0-113">Uma assinatura habilitada para logon único do Origami</span><span class="sxs-lookup"><span data-stu-id="668b0-113">An Origami single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="668b0-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="668b0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="668b0-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="668b0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="668b0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="668b0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="668b0-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="668b0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="668b0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="668b0-118">Scenario description</span></span>
<span data-ttu-id="668b0-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="668b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="668b0-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="668b0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="668b0-121">Adicionando Origami da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="668b0-121">Adding Origami from hello gallery</span></span>
2. <span data-ttu-id="668b0-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="668b0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-origami-from-hello-gallery"></a><span data-ttu-id="668b0-123">Adicionando Origami da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="668b0-123">Adding Origami from hello gallery</span></span>
<span data-ttu-id="668b0-124">integração de saudação tooconfigure de Origami no AD do Azure, você precisa tooadd Origami na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="668b0-124">tooconfigure hello integration of Origami into Azure AD, you need tooadd Origami from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="668b0-125">**tooadd Origami da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="668b0-125">**tooadd Origami from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="668b0-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="668b0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="668b0-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="668b0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="668b0-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="668b0-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="668b0-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="668b0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="668b0-133">Na caixa de pesquisa hello, digite **Origami**.</span><span class="sxs-lookup"><span data-stu-id="668b0-133">In hello search box, type **Origami**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/tutorial_origami_search.png)

5. <span data-ttu-id="668b0-135">No painel de resultados de saudação, selecione **Origami**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="668b0-135">In hello results panel, select **Origami**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/tutorial_origami_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="668b0-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="668b0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="668b0-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Origami, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="668b0-138">In this section, you configure and test Azure AD single sign-on with Origami based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="668b0-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Origami é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="668b0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Origami is tooa user in Azure AD.</span></span> <span data-ttu-id="668b0-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Origami precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="668b0-140">In other words, a link relationship between an Azure AD user and hello related user in Origami needs toobe established.</span></span>

<span data-ttu-id="668b0-141">Origami, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="668b0-141">In Origami, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="668b0-142">tooconfigure e teste de logon único do AD do Azure com Origami, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="668b0-142">tooconfigure and test Azure AD single sign-on with Origami, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="668b0-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="668b0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="668b0-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="668b0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="668b0-145">**[Criar um usuário de teste Origami](#creating-an-origami-test-user)**  -toohave um equivalente do Britta Simon em Origami é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="668b0-145">**[Creating an Origami test user](#creating-an-origami-test-user)** - toohave a counterpart of Britta Simon in Origami that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="668b0-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="668b0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="668b0-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="668b0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="668b0-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="668b0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="668b0-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Origami.</span><span class="sxs-lookup"><span data-stu-id="668b0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Origami application.</span></span>

<span data-ttu-id="668b0-150">**tooconfigure AD do Azure-logon único com Origami, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="668b0-150">**tooconfigure Azure AD single sign-on with Origami, perform hello following steps:**</span></span>

1. <span data-ttu-id="668b0-151">Em Olá portal do Azure, Olá **Origami** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="668b0-151">In hello Azure portal, on hello **Origami** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="668b0-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="668b0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_samlbase.png)

3. <span data-ttu-id="668b0-155">Em Olá **Origami domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="668b0-155">On hello **Origami Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_url.png)

    <span data-ttu-id="668b0-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://live.origamirisk.com/origami/account/login?account=<companyname>`</span><span class="sxs-lookup"><span data-stu-id="668b0-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://live.origamirisk.com/origami/account/login?account=<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="668b0-158">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="668b0-158">hello value is not real.</span></span> <span data-ttu-id="668b0-159">Valor de saudação de atualização com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="668b0-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="668b0-160">Entre em contato com [equipe de suporte de cliente Origami](https://wordpress.org/support/theme/origami) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="668b0-160">Contact [Origami Client support team](https://wordpress.org/support/theme/origami) tooget hello value.</span></span> 
 
4. <span data-ttu-id="668b0-161">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="668b0-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_certificate.png) 

5. <span data-ttu-id="668b0-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="668b0-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="668b0-165">Em Olá **Origami configuração** seção, clique em **configurar Origami** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="668b0-165">On hello **Origami Configuration** section, click **Configure Origami** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="668b0-166">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="668b0-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_configure.png) 

7. <span data-ttu-id="668b0-168">Faça logon no toohello conta Origami com direitos de administrador.</span><span class="sxs-lookup"><span data-stu-id="668b0-168">Log in toohello Origami account with Admin rights.</span></span>

8. <span data-ttu-id="668b0-169">No menu de saudação na parte superior de saudação, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="668b0-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

9. <span data-ttu-id="668b0-171">Na página de diálogo de logon único na instalação hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="668b0-171">On hello Single Sign On Setup dialog page, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_531.png)

    <span data-ttu-id="668b0-173">a.</span><span class="sxs-lookup"><span data-stu-id="668b0-173">a.</span></span> <span data-ttu-id="668b0-174">Selecione **Habilitar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="668b0-174">Select **Enable Single Sign On**.</span></span>

    <span data-ttu-id="668b0-175">b.</span><span class="sxs-lookup"><span data-stu-id="668b0-175">b.</span></span> <span data-ttu-id="668b0-176">Em Olá **entrar URL do provedor de identidade da página** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="668b0-176">In hello **Identity Provider's Sign-in Page URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="668b0-177">c.</span><span class="sxs-lookup"><span data-stu-id="668b0-177">c.</span></span> <span data-ttu-id="668b0-178">Em Olá **URL da página de logout do provedor de identidade** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="668b0-178">In hello **Identity Provider's Sign-out Page URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="668b0-179">d.</span><span class="sxs-lookup"><span data-stu-id="668b0-179">d.</span></span> <span data-ttu-id="668b0-180">Clique em **procurar** certificado de saudação tooupload que baixou do portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="668b0-180">Click **Browse** tooupload hello certificate you have downloaded from hello Azure portal.</span></span>

    <span data-ttu-id="668b0-181">e.</span><span class="sxs-lookup"><span data-stu-id="668b0-181">e.</span></span> <span data-ttu-id="668b0-182">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="668b0-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="668b0-183">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="668b0-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="668b0-184">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="668b0-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="668b0-185">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="668b0-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="668b0-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="668b0-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="668b0-187">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="668b0-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="668b0-189">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="668b0-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="668b0-190">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="668b0-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="668b0-192">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="668b0-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="668b0-194">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="668b0-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="668b0-196">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="668b0-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-origami-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="668b0-198">a.</span><span class="sxs-lookup"><span data-stu-id="668b0-198">a.</span></span> <span data-ttu-id="668b0-199">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="668b0-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="668b0-200">b.</span><span class="sxs-lookup"><span data-stu-id="668b0-200">b.</span></span> <span data-ttu-id="668b0-201">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="668b0-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="668b0-202">c.</span><span class="sxs-lookup"><span data-stu-id="668b0-202">c.</span></span> <span data-ttu-id="668b0-203">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="668b0-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="668b0-204">d.</span><span class="sxs-lookup"><span data-stu-id="668b0-204">d.</span></span> <span data-ttu-id="668b0-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="668b0-205">Click **Create**.</span></span>
 
### <a name="creating-an-origami-test-user"></a><span data-ttu-id="668b0-206">Criando um usuário de teste do Origami</span><span class="sxs-lookup"><span data-stu-id="668b0-206">Creating an Origami test user</span></span>

<span data-ttu-id="668b0-207">Nesta seção, você criará um usuário chamado Brenda Fernandes no Origami.</span><span class="sxs-lookup"><span data-stu-id="668b0-207">In this section, you create a user called Britta Simon in Origami.</span></span> 

1. <span data-ttu-id="668b0-208">Faça logon no toohello conta Origami com direitos de administrador.</span><span class="sxs-lookup"><span data-stu-id="668b0-208">Log in toohello Origami account with Admin rights.</span></span>

2. <span data-ttu-id="668b0-209">No menu de saudação na parte superior de saudação, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="668b0-209">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_51.png)

3. <span data-ttu-id="668b0-211">Em Olá **usuários e segurança** caixa de diálogo, clique em **usuários**.</span><span class="sxs-lookup"><span data-stu-id="668b0-211">On hello **Users and Security** dialog, click **Users**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_54.png)

4. <span data-ttu-id="668b0-213">Clique em **Adicionar Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="668b0-213">Click **Add New User**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_55.png)

5. <span data-ttu-id="668b0-215">Na caixa de diálogo de adicionar novo usuário hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="668b0-215">On hello Add New User dialog, perform hello following steps:</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_56.png)

    <span data-ttu-id="668b0-217">a.</span><span class="sxs-lookup"><span data-stu-id="668b0-217">a.</span></span> <span data-ttu-id="668b0-218">Em Olá **nome de usuário** caixa de texto, insira o email de saudação do usuário como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="668b0-218">In hello **User Name** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="668b0-219">b.</span><span class="sxs-lookup"><span data-stu-id="668b0-219">b.</span></span> <span data-ttu-id="668b0-220">Em Olá **senha** caixa de texto, digite uma senha.</span><span class="sxs-lookup"><span data-stu-id="668b0-220">In hello **Password** textbox, type a password.</span></span>

    <span data-ttu-id="668b0-221">c.</span><span class="sxs-lookup"><span data-stu-id="668b0-221">c.</span></span> <span data-ttu-id="668b0-222">Em Olá **Confirmar senha** caixa de texto, digite a senha de saudação novamente.</span><span class="sxs-lookup"><span data-stu-id="668b0-222">In hello **Confirm Password** textbox, type hello password again.</span></span>

    <span data-ttu-id="668b0-223">d.</span><span class="sxs-lookup"><span data-stu-id="668b0-223">d.</span></span> <span data-ttu-id="668b0-224">Em Olá **nome** caixa de texto, digite Olá primeiro nome do usuário, como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="668b0-224">In hello **First Name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="668b0-225">e.</span><span class="sxs-lookup"><span data-stu-id="668b0-225">e.</span></span> <span data-ttu-id="668b0-226">Em Olá **Sobrenome** caixa de texto, digite o sobrenome de saudação do usuário como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="668b0-226">In hello **Last Name** textbox, enter hello last name of user like **Simon**.</span></span>

    <span data-ttu-id="668b0-227">f.</span><span class="sxs-lookup"><span data-stu-id="668b0-227">f.</span></span> <span data-ttu-id="668b0-228">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="668b0-228">Click **Save**.</span></span>
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_57.png)

6. <span data-ttu-id="668b0-230">Atribuir **funções de usuário** e **acesso para cliente** toohello usuário.</span><span class="sxs-lookup"><span data-stu-id="668b0-230">Assign **User Roles** and **Client Access** toohello user.</span></span> 
   
    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_58.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="668b0-232">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="668b0-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="668b0-233">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooOrigami.</span><span class="sxs-lookup"><span data-stu-id="668b0-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOrigami.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="668b0-235">**tooassign Britta Simon tooOrigami, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="668b0-235">**tooassign Britta Simon tooOrigami, perform hello following steps:**</span></span>

1. <span data-ttu-id="668b0-236">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="668b0-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="668b0-238">Na lista de aplicativos hello, selecione **Origami**.</span><span class="sxs-lookup"><span data-stu-id="668b0-238">In hello applications list, select **Origami**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-origami-tutorial/tutorial_origami_app.png) 

3. <span data-ttu-id="668b0-240">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="668b0-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="668b0-242">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="668b0-242">Click **Add** button.</span></span> <span data-ttu-id="668b0-243">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="668b0-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="668b0-245">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="668b0-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="668b0-246">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="668b0-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="668b0-247">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="668b0-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="668b0-248">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="668b0-248">Testing single sign-on</span></span>

<span data-ttu-id="668b0-249">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="668b0-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="668b0-250">Quando você clica em bloco Origami Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo de Origami.</span><span class="sxs-lookup"><span data-stu-id="668b0-250">When you click hello Origami tile in hello Access Panel, you should get automatically signed-on tooyour Origami application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="668b0-251">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="668b0-251">Additional resources</span></span>

* [<span data-ttu-id="668b0-252">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="668b0-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="668b0-253">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="668b0-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-origami-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-origami-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-origami-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-origami-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-origami-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-origami-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-origami-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-origami-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-origami-tutorial/tutorial_general_203.png

