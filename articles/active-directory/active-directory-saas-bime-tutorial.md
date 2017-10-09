---
title: "Tutorial: Integração do Azure Active Directory ao Bime | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Bime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bdcf0729-c880-4c95-b739-0f6345b17dd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: 1213725028dd8ce90f22fa6e9c50ffabebc8f3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bime"></a><span data-ttu-id="c1759-103">Tutorial: Integração do Azure Active Directory ao Bime</span><span class="sxs-lookup"><span data-stu-id="c1759-103">Tutorial: Azure Active Directory integration with Bime</span></span>

<span data-ttu-id="c1759-104">Neste tutorial, você aprenderá como toointegrate Bime com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c1759-104">In this tutorial, you learn how toointegrate Bime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c1759-105">Integrando o Bime com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1759-105">Integrating Bime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c1759-106">Você pode controlar no AD do Azure que tenha acesso tooBime</span><span class="sxs-lookup"><span data-stu-id="c1759-106">You can control in Azure AD who has access tooBime</span></span>
- <span data-ttu-id="c1759-107">Você pode habilitar seu usuários tooautomatically get conectado tooBime (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c1759-107">You can enable your users tooautomatically get signed-on tooBime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c1759-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c1759-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c1759-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c1759-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1759-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c1759-110">Prerequisites</span></span>

<span data-ttu-id="c1759-111">tooconfigure integração do AD do Azure com Bime, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1759-111">tooconfigure Azure AD integration with Bime, you need hello following items:</span></span>

- <span data-ttu-id="c1759-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c1759-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c1759-113">Uma assinatura do Bime habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="c1759-113">A Bime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c1759-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c1759-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c1759-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c1759-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c1759-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c1759-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c1759-117">Se não tiver um ambiente de avaliação do Azure AD, será possível obter uma versão de avaliação de um mês aqui: [Oferta de avaliação](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c1759-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c1759-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c1759-118">Scenario description</span></span>
<span data-ttu-id="c1759-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c1759-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c1759-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c1759-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c1759-121">Adicionando Bime da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c1759-121">Adding Bime from hello gallery</span></span>
2. <span data-ttu-id="c1759-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c1759-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bime-from-hello-gallery"></a><span data-ttu-id="c1759-123">Adicionando Bime da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="c1759-123">Adding Bime from hello gallery</span></span>
<span data-ttu-id="c1759-124">integração de saudação tooconfigure do Bime no AD do Azure, você precisa tooadd Bime da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c1759-124">tooconfigure hello integration of Bime into Azure AD, you need tooadd Bime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c1759-125">**tooadd Bime da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c1759-125">**tooadd Bime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1759-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c1759-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c1759-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c1759-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c1759-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c1759-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c1759-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c1759-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c1759-133">Na caixa de pesquisa hello, digite **Bime**.</span><span class="sxs-lookup"><span data-stu-id="c1759-133">In hello search box, type **Bime**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bime-tutorial/tutorial_bime_search.png)

5. <span data-ttu-id="c1759-135">No painel de resultados de saudação, selecione **Bime**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c1759-135">In hello results panel, select **Bime**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bime-tutorial/tutorial_bime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c1759-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c1759-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c1759-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Bime com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c1759-138">In this section, you configure and test Azure AD single sign-on with Bime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c1759-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Bime é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1759-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bime is tooa user in Azure AD.</span></span> <span data-ttu-id="c1759-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Bime precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c1759-140">In other words, a link relationship between an Azure AD user and hello related user in Bime needs toobe established.</span></span>

<span data-ttu-id="c1759-141">No Bime, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="c1759-141">In Bime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="c1759-142">tooconfigure e teste de logon único do AD do Azure com Bime, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1759-142">tooconfigure and test Azure AD single sign-on with Bime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c1759-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c1759-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c1759-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c1759-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c1759-145">**[Criar um usuário de teste do Bime](#creating-a-bime-test-user)**  -toohave um equivalente do Britta Simon no Bime é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c1759-145">**[Creating a Bime test user](#creating-a-bime-test-user)** - toohave a counterpart of Britta Simon in Bime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c1759-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c1759-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c1759-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c1759-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c1759-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c1759-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c1759-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Bime.</span><span class="sxs-lookup"><span data-stu-id="c1759-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bime application.</span></span>

<span data-ttu-id="c1759-150">**tooconfigure AD do Azure-logon único com Bime, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c1759-150">**tooconfigure Azure AD single sign-on with Bime, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1759-151">Em Olá portal do Azure, Olá **Bime** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c1759-151">In hello Azure portal, on hello **Bime** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c1759-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c1759-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-bime-tutorial/tutorial_bime_samlbase.png)

3. <span data-ttu-id="c1759-155">Em Olá **Bime domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1759-155">On hello **Bime Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bime-tutorial/tutorial_bime_url.png)

    <span data-ttu-id="c1759-157">a.</span><span class="sxs-lookup"><span data-stu-id="c1759-157">a.</span></span> <span data-ttu-id="c1759-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="c1759-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    <span data-ttu-id="c1759-159">b.</span><span class="sxs-lookup"><span data-stu-id="c1759-159">b.</span></span> <span data-ttu-id="c1759-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant-name>.Bimeapp.com`</span><span class="sxs-lookup"><span data-stu-id="c1759-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.Bimeapp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c1759-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="c1759-161">These values are not real.</span></span> <span data-ttu-id="c1759-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="c1759-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c1759-163">Entre em contato com [equipe de suporte do cliente Bime](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="c1759-163">Contact [Bime Client support team](https://bime.zendesk.com/hc/categories/202604307-Support-tech-notes-and-tips-) tooget these values.</span></span> 
 
4. <span data-ttu-id="c1759-164">Em Olá **o certificado de autenticação SAML** seção, Olá cópia **impressão digital** valor de certificado hello.</span><span class="sxs-lookup"><span data-stu-id="c1759-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value from hello certificate.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bime-tutorial/tutorial_bime_certificate.png) 

5. <span data-ttu-id="c1759-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c1759-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c1759-168">Em Olá **Bime configuração** seção, clique em **configurar Bime** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="c1759-168">On hello **Bime Configuration** section, click **Configure Bime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="c1759-169">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="c1759-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bime-tutorial/tutorial_bime_configure.png) 

7. <span data-ttu-id="c1759-171">Em outra janela do navegador da Web, faça logon em seu site de empresa Bime como um administrador.</span><span class="sxs-lookup"><span data-stu-id="c1759-171">In a different web browser window, log into your Bime company site as an administrator.</span></span>

8. <span data-ttu-id="c1759-172">Na barra de ferramentas hello, clique em **Admin**e, em seguida, **conta**.</span><span class="sxs-lookup"><span data-stu-id="c1759-172">In hello toolbar, click **Admin**, and then **Account**.</span></span>
   
    <span data-ttu-id="c1759-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c1759-173">![Admin](./media/active-directory-saas-bime-tutorial/ic775558.png "Admin")</span></span>

9. <span data-ttu-id="c1759-174">Na página de configuração de conta hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1759-174">On hello account configuration page, perform hello following steps:</span></span>
   
    <span data-ttu-id="c1759-175">![Configurar Logon Único](./media/active-directory-saas-bime-tutorial/ic775559.png "Configurar Logon Único")</span><span class="sxs-lookup"><span data-stu-id="c1759-175">![Configure Single Sign-On](./media/active-directory-saas-bime-tutorial/ic775559.png "Configure Single Sign-On")</span></span>
   
    <span data-ttu-id="c1759-176">a.</span><span class="sxs-lookup"><span data-stu-id="c1759-176">a.</span></span> <span data-ttu-id="c1759-177">Selecione **Habilitar autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="c1759-177">Select **Enable SAML authentication**.</span></span>

    <span data-ttu-id="c1759-178">b.</span><span class="sxs-lookup"><span data-stu-id="c1759-178">b.</span></span> <span data-ttu-id="c1759-179">Em Olá **URL de logon remoto** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1759-179">In hello **Remote Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c1759-180">c.</span><span class="sxs-lookup"><span data-stu-id="c1759-180">c.</span></span>  <span data-ttu-id="c1759-181">Saudação de colar **impressão digital** valor no portal do Azure em Olá **impressão digital do certificado** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="c1759-181">Paste hello **Thumbprint** value from Azure portal into hello **Certificate Fingerprint** textbox.</span></span>       
   
    <span data-ttu-id="c1759-182">d.</span><span class="sxs-lookup"><span data-stu-id="c1759-182">d.</span></span> <span data-ttu-id="c1759-183">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c1759-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="c1759-184">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c1759-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c1759-185">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c1759-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c1759-186">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c1759-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c1759-187">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c1759-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="c1759-188">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1759-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c1759-190">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c1759-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1759-191">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c1759-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c1759-193">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c1759-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c1759-195">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c1759-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c1759-197">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1759-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-bime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c1759-199">a.</span><span class="sxs-lookup"><span data-stu-id="c1759-199">a.</span></span> <span data-ttu-id="c1759-200">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c1759-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c1759-201">b.</span><span class="sxs-lookup"><span data-stu-id="c1759-201">b.</span></span> <span data-ttu-id="c1759-202">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c1759-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c1759-203">c.</span><span class="sxs-lookup"><span data-stu-id="c1759-203">c.</span></span> <span data-ttu-id="c1759-204">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c1759-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c1759-205">d.</span><span class="sxs-lookup"><span data-stu-id="c1759-205">d.</span></span> <span data-ttu-id="c1759-206">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c1759-206">Click **Create**.</span></span>
 
### <a name="creating-a-bime-test-user"></a><span data-ttu-id="c1759-207">Criação de um usuário de teste do Bime</span><span class="sxs-lookup"><span data-stu-id="c1759-207">Creating a Bime test user</span></span>

<span data-ttu-id="c1759-208">Em ordem tooenable AD do Azure usuários toolog em tooBime, eles devem ser provisionados no Bime.</span><span class="sxs-lookup"><span data-stu-id="c1759-208">In order tooenable Azure AD users toolog in tooBime, they must be provisioned into Bime.</span></span> <span data-ttu-id="c1759-209">No caso de saudação do Bime, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="c1759-209">In hello case of Bime, provisioning is a manual task.</span></span>

<span data-ttu-id="c1759-210">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c1759-210">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1759-211">Faça logon no tooyour **Bime** locatário.</span><span class="sxs-lookup"><span data-stu-id="c1759-211">Log in tooyour **Bime** tenant.</span></span>

2. <span data-ttu-id="c1759-212">Na barra de ferramentas hello, clique em **Admin**e, em seguida, **usuários**.</span><span class="sxs-lookup"><span data-stu-id="c1759-212">In hello toolbar, click **Admin**, and then **Users**.</span></span>
   
    <span data-ttu-id="c1759-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span><span class="sxs-lookup"><span data-stu-id="c1759-213">![Admin](./media/active-directory-saas-bime-tutorial/ic775561.png "Admin")</span></span>

3. <span data-ttu-id="c1759-214">Em Olá **lista usuários**, clique em **adicionar novo usuário** ("+").</span><span class="sxs-lookup"><span data-stu-id="c1759-214">In hello **Users List**, click **Add New User** (“+”).</span></span>
   
    <span data-ttu-id="c1759-215">![Usuários](./media/active-directory-saas-bime-tutorial/ic775562.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="c1759-215">![Users](./media/active-directory-saas-bime-tutorial/ic775562.png "Users")</span></span>

4. <span data-ttu-id="c1759-216">Em Olá **detalhes do usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c1759-216">On hello **User Details** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="c1759-217">![Detalhes do Usuário](./media/active-directory-saas-bime-tutorial/ic775563.png "Detalhes do Usuário")</span><span class="sxs-lookup"><span data-stu-id="c1759-217">![User Details](./media/active-directory-saas-bime-tutorial/ic775563.png "User Details")</span></span>
   
    <span data-ttu-id="c1759-218">a.</span><span class="sxs-lookup"><span data-stu-id="c1759-218">a.</span></span> <span data-ttu-id="c1759-219">Em Olá **nome** caixa de texto, digite Olá primeiro nome do usuário, como **Britta**.</span><span class="sxs-lookup"><span data-stu-id="c1759-219">In hello **First name** textbox, enter hello first name of user like **Britta**.</span></span>

    <span data-ttu-id="c1759-220">b.</span><span class="sxs-lookup"><span data-stu-id="c1759-220">b.</span></span> <span data-ttu-id="c1759-221">Em Olá **Sobrenome** caixa de texto, digite o sobrenome de saudação do usuário como **Simon**.</span><span class="sxs-lookup"><span data-stu-id="c1759-221">In hello **Last name** textbox, enter hello last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="c1759-222">c.</span><span class="sxs-lookup"><span data-stu-id="c1759-222">c.</span></span> <span data-ttu-id="c1759-223">Em Olá **Email** caixa de texto, insira o email de saudação do usuário como  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="c1759-223">In hello **Email** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="c1759-224">d.</span><span class="sxs-lookup"><span data-stu-id="c1759-224">d.</span></span> <span data-ttu-id="c1759-225">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c1759-225">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="c1759-226">Você pode usar qualquer ferramenta de criação outros Bime usuário conta ou APIs fornecidas pelo Bime tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="c1759-226">You can use any other Bime user account creation tools or APIs provided by Bime tooprovision AAD user accounts.</span></span>
>  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c1759-227">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c1759-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c1759-228">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBime.</span><span class="sxs-lookup"><span data-stu-id="c1759-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBime.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c1759-230">**tooassign Britta Simon tooBime, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c1759-230">**tooassign Britta Simon tooBime, perform hello following steps:**</span></span>

1. <span data-ttu-id="c1759-231">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c1759-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c1759-233">Na lista de aplicativos hello, selecione **Bime**.</span><span class="sxs-lookup"><span data-stu-id="c1759-233">In hello applications list, select **Bime**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-bime-tutorial/tutorial_bime_app.png) 

3. <span data-ttu-id="c1759-235">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c1759-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c1759-237">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c1759-237">Click **Add** button.</span></span> <span data-ttu-id="c1759-238">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c1759-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c1759-240">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c1759-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c1759-241">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c1759-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c1759-242">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c1759-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c1759-243">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c1759-243">Testing single sign-on</span></span>

<span data-ttu-id="c1759-244">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="c1759-244">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c1759-245">Quando você clica em bloco Bime Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Bime aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c1759-245">When you click hello Bime tile in hello Access Panel, you should get automatically signed-on tooyour Bime application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c1759-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c1759-246">Additional resources</span></span>

* [<span data-ttu-id="c1759-247">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c1759-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c1759-248">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c1759-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bime-tutorial/tutorial_general_203.png

