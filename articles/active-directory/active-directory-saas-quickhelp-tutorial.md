---
title: "Tutorial: Integração do Azure Active Directory com o QuickHelp | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e da ajuda rápida."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: bbde5eb9bdad89680923ccd36c321b6923f91789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="1246b-103">Tutorial: Integração do Active Directory do Azure com o QuickHelp</span><span class="sxs-lookup"><span data-stu-id="1246b-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="1246b-104">Neste tutorial, você aprenderá como toointegrate da ajuda rápida com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="1246b-104">In this tutorial, you learn how toointegrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1246b-105">Integração da ajuda rápida com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="1246b-105">Integrating QuickHelp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1246b-106">Você pode controlar no AD do Azure que tenha acesso tooQuickHelp</span><span class="sxs-lookup"><span data-stu-id="1246b-106">You can control in Azure AD who has access tooQuickHelp</span></span>
- <span data-ttu-id="1246b-107">Você pode habilitar seu usuários tooautomatically get conectado tooQuickHelp (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1246b-107">You can enable your users tooautomatically get signed-on tooQuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1246b-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1246b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1246b-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1246b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1246b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1246b-110">Prerequisites</span></span>

<span data-ttu-id="1246b-111">tooconfigure integração do AD do Azure com da ajuda rápida, é necessário Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="1246b-111">tooconfigure Azure AD integration with QuickHelp, you need hello following items:</span></span>

- <span data-ttu-id="1246b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1246b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1246b-113">Uma assinatura habilitada para logon único do QuickHelp</span><span class="sxs-lookup"><span data-stu-id="1246b-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1246b-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="1246b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1246b-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="1246b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1246b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="1246b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1246b-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1246b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1246b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="1246b-118">Scenario description</span></span>
<span data-ttu-id="1246b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="1246b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1246b-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="1246b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1246b-121">Adição da ajuda rápida da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1246b-121">Adding QuickHelp from hello gallery</span></span>
2. <span data-ttu-id="1246b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1246b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-hello-gallery"></a><span data-ttu-id="1246b-123">Adição da ajuda rápida da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="1246b-123">Adding QuickHelp from hello gallery</span></span>
<span data-ttu-id="1246b-124">integração de saudação tooconfigure da ajuda rápida no AD do Azure, você precisa tooadd da ajuda rápida da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="1246b-124">tooconfigure hello integration of QuickHelp into Azure AD, you need tooadd QuickHelp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1246b-125">**tooadd da ajuda rápida da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1246b-125">**tooadd QuickHelp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1246b-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1246b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1246b-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="1246b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1246b-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1246b-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="1246b-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1246b-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="1246b-133">Na caixa de pesquisa hello, digite **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="1246b-133">In hello search box, type **QuickHelp**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="1246b-135">No painel de resultados de saudação, selecione **QuickHelp**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1246b-135">In hello results panel, select **QuickHelp**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1246b-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1246b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1246b-138">Nesta seção, você configura e testa o logon único do Azure AD com o QuickHelp, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="1246b-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1246b-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá da ajuda rápida é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1246b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp is tooa user in Azure AD.</span></span> <span data-ttu-id="1246b-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação da ajuda rápida precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1246b-140">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="1246b-141">Da ajuda rápida, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="1246b-141">In QuickHelp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1246b-142">tooconfigure e teste de logon único do AD do Azure com da ajuda rápida, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="1246b-142">tooconfigure and test Azure AD single sign-on with QuickHelp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1246b-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="1246b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1246b-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1246b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1246b-145">**[Criar um usuário de teste da ajuda rápida](#creating-a-quickhelp-test-user)**  -toohave um equivalente do Britta Simon da ajuda rápida que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="1246b-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - toohave a counterpart of Britta Simon in QuickHelp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1246b-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="1246b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1246b-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="1246b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1246b-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="1246b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1246b-149">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo da ajuda rápida.</span><span class="sxs-lookup"><span data-stu-id="1246b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="1246b-150">**tooconfigure AD do Azure-logon único da ajuda rápida, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1246b-150">**tooconfigure Azure AD single sign-on with QuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="1246b-151">Em Olá portal do Azure, Olá **QuickHelp** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="1246b-151">In hello Azure portal, on hello **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="1246b-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="1246b-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="1246b-155">Em Olá **URLs e domínio da ajuda rápida** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1246b-155">On hello **QuickHelp Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="1246b-157">a.</span><span class="sxs-lookup"><span data-stu-id="1246b-157">a.</span></span> <span data-ttu-id="1246b-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="1246b-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="1246b-159">b.</span><span class="sxs-lookup"><span data-stu-id="1246b-159">b.</span></span> <span data-ttu-id="1246b-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="1246b-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1246b-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="1246b-161">These values are not real.</span></span> <span data-ttu-id="1246b-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="1246b-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1246b-163">Entre em contato com [a equipe de suporte da ajuda rápida cliente](https://support.quickhelp.com/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="1246b-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="1246b-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="1246b-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="1246b-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="1246b-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="1246b-168">Site de empresa da ajuda rápida de tooyour logon como administrador.</span><span class="sxs-lookup"><span data-stu-id="1246b-168">Sign-on tooyour QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="1246b-169">No menu de saudação na parte superior de saudação, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="1246b-169">In hello menu on hello top, click **Admin**.</span></span>
   
    ![Configurar Logon Único][21]

8. <span data-ttu-id="1246b-171">Em Olá **QuickHelp Admin** menu, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="1246b-171">In hello **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Configurar Logon Único][22]

9. <span data-ttu-id="1246b-173">Clique em **Configurações da Autenticação**.</span><span class="sxs-lookup"><span data-stu-id="1246b-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="1246b-174">Em Olá **configurações de autenticação** página, execute Olá etapas</span><span class="sxs-lookup"><span data-stu-id="1246b-174">On hello **Authentication Settings** page, perform hello following steps</span></span>
   
    ![Configurar Logon Único][23]
   
    <span data-ttu-id="1246b-176">a.</span><span class="sxs-lookup"><span data-stu-id="1246b-176">a.</span></span> <span data-ttu-id="1246b-177">Como **Tipo de SSO**, selecione **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="1246b-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="1246b-178">b.</span><span class="sxs-lookup"><span data-stu-id="1246b-178">b.</span></span> <span data-ttu-id="1246b-179">tooupload seu arquivo de metadados do Azure baixado, clique em **procurar**, navegue arquivo toohello, finalizar clique **carregar metadados**.</span><span class="sxs-lookup"><span data-stu-id="1246b-179">tooupload your downloaded Azure metadata file, click **Browse**, navigate toohello file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="1246b-180">c.</span><span class="sxs-lookup"><span data-stu-id="1246b-180">c.</span></span> <span data-ttu-id="1246b-181">Em Olá **Email** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="1246b-181">In hello **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="1246b-182">d.</span><span class="sxs-lookup"><span data-stu-id="1246b-182">d.</span></span> <span data-ttu-id="1246b-183">Em Olá **nome** caixa de texto, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="1246b-183">In hello **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="1246b-184">e.</span><span class="sxs-lookup"><span data-stu-id="1246b-184">e.</span></span> <span data-ttu-id="1246b-185">Em Olá **Sobrenome** caixa de texto, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="1246b-185">In hello **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="1246b-186">f.</span><span class="sxs-lookup"><span data-stu-id="1246b-186">f.</span></span> <span data-ttu-id="1246b-187">Em Olá **barra de ação**, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="1246b-187">In hello **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="1246b-188">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="1246b-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1246b-189">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="1246b-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1246b-190">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1246b-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1246b-191">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1246b-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="1246b-192">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1246b-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="1246b-194">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1246b-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1246b-195">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="1246b-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1246b-197">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="1246b-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1246b-199">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1246b-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1246b-201">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1246b-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1246b-203">a.</span><span class="sxs-lookup"><span data-stu-id="1246b-203">a.</span></span> <span data-ttu-id="1246b-204">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1246b-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1246b-205">b.</span><span class="sxs-lookup"><span data-stu-id="1246b-205">b.</span></span> <span data-ttu-id="1246b-206">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1246b-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1246b-207">c.</span><span class="sxs-lookup"><span data-stu-id="1246b-207">c.</span></span> <span data-ttu-id="1246b-208">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="1246b-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1246b-209">d.</span><span class="sxs-lookup"><span data-stu-id="1246b-209">d.</span></span> <span data-ttu-id="1246b-210">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1246b-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="1246b-211">Criando um usuário de teste do QuickHelp</span><span class="sxs-lookup"><span data-stu-id="1246b-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="1246b-212">Olá o objetivo desta seção é toocreate um usuário chamado Britta Simon da ajuda rápida.</span><span class="sxs-lookup"><span data-stu-id="1246b-212">hello objective of this section is toocreate a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="1246b-213">Para toowork de logon único, o AD do Azure precisa tooknow é qual usuário equivalente de saudação da ajuda rápida tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1246b-213">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in QuickHelp tooa user in Azure AD is.</span></span> <span data-ttu-id="1246b-214">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação da ajuda rápida precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="1246b-214">In other words, a link relationship between an Azure AD user and hello related user in QuickHelp needs toobe established.</span></span>

<span data-ttu-id="1246b-215">O QuickHelp dá suporte ao provisionamento just-in-time.</span><span class="sxs-lookup"><span data-stu-id="1246b-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="1246b-216">Isso significa que, se necessário, uma conta de usuário é criada automaticamente da ajuda rápida e conta Olá é vinculado toohello conta AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="1246b-216">This means, if necessary, a user account is automatically created in QuickHelp and hello account is linked toohello Azure AD account.</span></span>

<span data-ttu-id="1246b-217">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="1246b-217">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1246b-218">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="1246b-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1246b-219">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooQuickHelp.</span><span class="sxs-lookup"><span data-stu-id="1246b-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQuickHelp.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="1246b-221">**tooassign Britta Simon tooQuickHelp, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="1246b-221">**tooassign Britta Simon tooQuickHelp, perform hello following steps:**</span></span>

1. <span data-ttu-id="1246b-222">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="1246b-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="1246b-224">Na lista de aplicativos hello, selecione **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="1246b-224">In hello applications list, select **QuickHelp**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="1246b-226">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="1246b-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="1246b-228">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1246b-228">Click **Add** button.</span></span> <span data-ttu-id="1246b-229">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1246b-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="1246b-231">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="1246b-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1246b-232">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1246b-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1246b-233">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1246b-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1246b-234">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="1246b-234">Testing single sign-on</span></span>

<span data-ttu-id="1246b-235">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="1246b-235">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>  

<span data-ttu-id="1246b-236">Quando você clica em um bloco da ajuda rápida Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour da ajuda rápida aplicativo.</span><span class="sxs-lookup"><span data-stu-id="1246b-236">When you click hello QuickHelp tile in hello Access Panel, you should get automatically signed-on tooyour QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="1246b-237">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="1246b-237">Additional resources</span></span>

* [<span data-ttu-id="1246b-238">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="1246b-238">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1246b-239">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1246b-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
