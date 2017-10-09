---
title: "Tutorial: Integração do Azure Active Directory com o Syncplicity | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 6148112a959232ed24d76d1c7b8773f06568fee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="9407d-103">Tutorial: Integração do Active Directory do Azure com o Syncplicity</span><span class="sxs-lookup"><span data-stu-id="9407d-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="9407d-104">Neste tutorial, você aprenderá como toointegrate Syncplicity com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="9407d-104">In this tutorial, you learn how toointegrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9407d-105">Integrando o Syncplicity com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="9407d-105">Integrating Syncplicity with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9407d-106">Você pode controlar no AD do Azure que tenha acesso tooSyncplicity</span><span class="sxs-lookup"><span data-stu-id="9407d-106">You can control in Azure AD who has access tooSyncplicity</span></span>
- <span data-ttu-id="9407d-107">Você pode habilitar seu usuários tooautomatically get conectado tooSyncplicity (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9407d-107">You can enable your users tooautomatically get signed-on tooSyncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9407d-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9407d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9407d-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9407d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9407d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9407d-110">Prerequisites</span></span>

<span data-ttu-id="9407d-111">tooconfigure integração do AD do Azure com o Syncplicity, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="9407d-111">tooconfigure Azure AD integration with Syncplicity, you need hello following items:</span></span>

- <span data-ttu-id="9407d-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9407d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9407d-113">Uma assinatura habilitada para logon único do Syncplicity</span><span class="sxs-lookup"><span data-stu-id="9407d-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9407d-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="9407d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9407d-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="9407d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9407d-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="9407d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9407d-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9407d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9407d-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="9407d-118">Scenario description</span></span>
<span data-ttu-id="9407d-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="9407d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9407d-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="9407d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9407d-121">Adicionando Syncplicity da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9407d-121">Adding Syncplicity from hello gallery</span></span>
2. <span data-ttu-id="9407d-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9407d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-hello-gallery"></a><span data-ttu-id="9407d-123">Adicionando Syncplicity da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="9407d-123">Adding Syncplicity from hello gallery</span></span>
<span data-ttu-id="9407d-124">integração de saudação tooconfigure do Syncplicity no AD do Azure, você precisa tooadd Syncplicity da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="9407d-124">tooconfigure hello integration of Syncplicity into Azure AD, you need tooadd Syncplicity from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9407d-125">**tooadd Syncplicity da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9407d-125">**tooadd Syncplicity from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9407d-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9407d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9407d-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="9407d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9407d-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9407d-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="9407d-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9407d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="9407d-133">Na caixa de pesquisa hello, digite **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="9407d-133">In hello search box, type **Syncplicity**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="9407d-135">No painel de resultados de saudação, selecione **Syncplicity**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="9407d-135">In hello results panel, select **Syncplicity**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9407d-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9407d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9407d-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Syncplicity, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="9407d-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9407d-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Syncplicity é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="9407d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Syncplicity is tooa user in Azure AD.</span></span> <span data-ttu-id="9407d-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Syncplicity precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="9407d-140">In other words, a link relationship between an Azure AD user and hello related user in Syncplicity needs toobe established.</span></span>

<span data-ttu-id="9407d-141">No Syncplicity, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="9407d-141">In Syncplicity, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9407d-142">tooconfigure e teste de logon único do AD do Azure com o Syncplicity, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="9407d-142">tooconfigure and test Azure AD single sign-on with Syncplicity, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9407d-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9407d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9407d-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9407d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9407d-145">**[Criar um usuário de teste do Syncplicity](#creating-a-syncplicity-test-user)**  -toohave um equivalente do Britta Simon no Syncplicity que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="9407d-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - toohave a counterpart of Britta Simon in Syncplicity that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9407d-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="9407d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9407d-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="9407d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9407d-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="9407d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9407d-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="9407d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="9407d-150">**tooconfigure AD do Azure-logon único com o Syncplicity, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9407d-150">**tooconfigure Azure AD single sign-on with Syncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="9407d-151">Em Olá portal do Azure, Olá **Syncplicity** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="9407d-151">In hello Azure portal, on hello **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="9407d-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="9407d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="9407d-155">Em Olá **Syncplicity domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9407d-155">On hello **Syncplicity Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="9407d-157">a.</span><span class="sxs-lookup"><span data-stu-id="9407d-157">a.</span></span> <span data-ttu-id="9407d-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="9407d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="9407d-159">b.</span><span class="sxs-lookup"><span data-stu-id="9407d-159">b.</span></span> <span data-ttu-id="9407d-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="9407d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9407d-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="9407d-161">These values are not real.</span></span> <span data-ttu-id="9407d-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="9407d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="9407d-163">Entre em contato com [equipe de suporte do cliente do Syncplicity](https://www.syncplicity.com/contact-us) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="9407d-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) tooget these values.</span></span> 
 

4. <span data-ttu-id="9407d-164">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="9407d-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="9407d-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="9407d-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9407d-168">Em Olá **Syncplicity configuração** seção, clique em **configurar Syncplicity** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="9407d-168">On hello **Syncplicity Configuration** section, click **Configure Syncplicity** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9407d-169">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="9407d-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="9407d-171">Entrar tooyour **Syncplicity** locatário.</span><span class="sxs-lookup"><span data-stu-id="9407d-171">Sign in tooyour **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="9407d-172">No menu de saudação na parte superior de saudação, clique em **admin**, selecione **configurações**e, em seguida, clique em **domínio personalizado e logon único**.</span><span class="sxs-lookup"><span data-stu-id="9407d-172">In hello menu on hello top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="9407d-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="9407d-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="9407d-174">Em Olá **Single Sign-On (SSO)** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9407d-174">On hello **Single Sign-On (SSO)** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="9407d-175">![Logon Único \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="9407d-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="9407d-176">a.</span><span class="sxs-lookup"><span data-stu-id="9407d-176">a.</span></span> <span data-ttu-id="9407d-177">Em Olá **domínio personalizado** caixa de texto, nome de saudação do tipo do seu domínio.</span><span class="sxs-lookup"><span data-stu-id="9407d-177">In hello **Custom Domain** textbox, type hello name of your domain.</span></span>
  
    <span data-ttu-id="9407d-178">b.</span><span class="sxs-lookup"><span data-stu-id="9407d-178">b.</span></span> <span data-ttu-id="9407d-179">Selecione **Habilitado** como **Status do Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="9407d-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="9407d-180">c.</span><span class="sxs-lookup"><span data-stu-id="9407d-180">c.</span></span> <span data-ttu-id="9407d-181">Em Olá **Id da entidade** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9407d-181">In hello **Entity Id** textbox, Paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9407d-182">d.</span><span class="sxs-lookup"><span data-stu-id="9407d-182">d.</span></span> <span data-ttu-id="9407d-183">Em Olá **URL da página de entrada** caixa de texto, Olá colar **Single Sign-On URL do serviço SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9407d-183">In hello **Sign-in page URL** textbox, Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9407d-184">e.</span><span class="sxs-lookup"><span data-stu-id="9407d-184">e.</span></span> <span data-ttu-id="9407d-185">Em Olá **URL da página de Logout** caixa de texto, Olá colar **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9407d-185">In hello **Logout page URL** textbox, Paste hello **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="9407d-186">f.</span><span class="sxs-lookup"><span data-stu-id="9407d-186">f.</span></span> <span data-ttu-id="9407d-187">Em **certificado do provedor de identidade**, clique em **Escolher arquivo**e, em seguida, carregue o certificado de saudação que você baixou do portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="9407d-187">In **Identity Provider Certificate**, click **Choose file**, and then upload hello certificate which you have downloaded from hello Azure portal.</span></span> 

    <span data-ttu-id="9407d-188">g.</span><span class="sxs-lookup"><span data-stu-id="9407d-188">g.</span></span> <span data-ttu-id="9407d-189">Clique em **SALVAR ALTERAÇÕES**.</span><span class="sxs-lookup"><span data-stu-id="9407d-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="9407d-190">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="9407d-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9407d-191">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="9407d-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9407d-192">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9407d-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9407d-193">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9407d-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="9407d-194">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9407d-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="9407d-196">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9407d-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9407d-197">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="9407d-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9407d-199">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="9407d-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9407d-201">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="9407d-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9407d-203">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9407d-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9407d-205">a.</span><span class="sxs-lookup"><span data-stu-id="9407d-205">a.</span></span> <span data-ttu-id="9407d-206">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9407d-206">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9407d-207">b.</span><span class="sxs-lookup"><span data-stu-id="9407d-207">b.</span></span> <span data-ttu-id="9407d-208">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9407d-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9407d-209">c.</span><span class="sxs-lookup"><span data-stu-id="9407d-209">c.</span></span> <span data-ttu-id="9407d-210">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="9407d-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9407d-211">d.</span><span class="sxs-lookup"><span data-stu-id="9407d-211">d.</span></span> <span data-ttu-id="9407d-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9407d-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="9407d-213">Criar um usuário de teste do Syncplicity</span><span class="sxs-lookup"><span data-stu-id="9407d-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="9407d-214">Para AAD usuários toobe capaz de toosign no, eles devem ser provisionados tooSyncplicity aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9407d-214">For AAD users toobe able toosign in, they must be provisioned tooSyncplicity application.</span></span> <span data-ttu-id="9407d-215">Esta seção descreve como contas de usuário do AAD toocreate no Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="9407d-215">This section describes how toocreate AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="9407d-216">**tooprovision um tooSyncplicity de conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9407d-216">**tooprovision a user account tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="9407d-217">Faça logon no tooyour **Syncplicity** locatário (por exemplo: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="9407d-217">Log in tooyour **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="9407d-218">Clique em **Administrador** e selecione **Contas de Usuário**.</span><span class="sxs-lookup"><span data-stu-id="9407d-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="9407d-219">Clique em **ADICIONAR UM USUÁRIO**.</span><span class="sxs-lookup"><span data-stu-id="9407d-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="9407d-220">![Gerenciar Usuários](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Gerenciar Usuários")</span><span class="sxs-lookup"><span data-stu-id="9407d-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="9407d-221">Saudação de tipo **endereços de Email** de uma conta do AAD que você deseja tooprovision, selecione **usuário** como **função**e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="9407d-221">Type hello **Email addressess** of an AAD account you want tooprovision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="9407d-222">![Dados da Conta](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Dados da Conta")</span><span class="sxs-lookup"><span data-stu-id="9407d-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="9407d-223">proprietário de conta do AAD Olá obtém um email incluindo um link tooconfirm e ativar conta hello.</span><span class="sxs-lookup"><span data-stu-id="9407d-223">hello AAD account holder  gets an email including a link tooconfirm and activate hello account.</span></span> 
    > 

5. <span data-ttu-id="9407d-224">Selecione um grupo em sua empresa do qual o novo usuário deverá se tornar membro e clique em **AVANÇAR**.</span><span class="sxs-lookup"><span data-stu-id="9407d-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="9407d-225">![Associação a um Grupo](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Associação a um Grupo")</span><span class="sxs-lookup"><span data-stu-id="9407d-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="9407d-226">Se não houver nenhum grupo listado, basta clicar em **AVANÇAR**.</span><span class="sxs-lookup"><span data-stu-id="9407d-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="9407d-227">Selecione as pastas Olá seria como tooplace sob controle do Syncplicity no computador do usuário hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="9407d-227">Select hello folders you would like tooplace under Syncplicity’s control on hello user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="9407d-228">![Pastas do Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Pastas do Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="9407d-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="9407d-229">Você pode usar qualquer ferramenta de criação outros Syncplicity usuário conta ou APIs fornecidas pelo Syncplicity tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="9407d-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9407d-230">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="9407d-230">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9407d-231">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSyncplicity.</span><span class="sxs-lookup"><span data-stu-id="9407d-231">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSyncplicity.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="9407d-233">**tooassign Britta Simon tooSyncplicity, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="9407d-233">**tooassign Britta Simon tooSyncplicity, perform hello following steps:**</span></span>

1. <span data-ttu-id="9407d-234">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="9407d-234">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="9407d-236">Na lista de aplicativos hello, selecione **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="9407d-236">In hello applications list, select **Syncplicity**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="9407d-238">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="9407d-238">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="9407d-240">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9407d-240">Click **Add** button.</span></span> <span data-ttu-id="9407d-241">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9407d-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="9407d-243">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="9407d-243">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9407d-244">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9407d-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9407d-245">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="9407d-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9407d-246">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="9407d-246">Testing single sign-on</span></span>

<span data-ttu-id="9407d-247">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="9407d-247">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9407d-248">Quando você clica em bloco Syncplicity Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Syncplicity aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9407d-248">When you click hello Syncplicity tile in hello Access Panel, you should get automatically signed-on tooyour Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="9407d-249">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="9407d-249">Additional resources</span></span>

* [<span data-ttu-id="9407d-250">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9407d-250">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9407d-251">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9407d-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

