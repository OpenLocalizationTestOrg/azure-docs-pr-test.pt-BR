---
title: "Tutorial: Integração do Azure Active Directory ao New Relic | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o New Relic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: dc8f0df3b18a32bde155e8911a581fc5f91af217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="d4fb6-103">Tutorial: Integração do Active Directory do Azure com o New Relic</span><span class="sxs-lookup"><span data-stu-id="d4fb6-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="d4fb6-104">Neste tutorial, você aprenderá como toointegrate New Relic com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="d4fb6-104">In this tutorial, you learn how toointegrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d4fb6-105">Integrando o New Relic com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4fb6-105">Integrating New Relic with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d4fb6-106">Você pode controlar no AD do Azure que tenha acesso tooNew Relic</span><span class="sxs-lookup"><span data-stu-id="d4fb6-106">You can control in Azure AD who has access tooNew Relic</span></span>
- <span data-ttu-id="d4fb6-107">Você pode habilitar seu usuários tooautomatically get conectado tooNew Relic (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d4fb6-107">You can enable your users tooautomatically get signed-on tooNew Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d4fb6-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d4fb6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d4fb6-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d4fb6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4fb6-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d4fb6-110">Prerequisites</span></span>

<span data-ttu-id="d4fb6-111">tooconfigure integração do AD do Azure com o New Relic, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4fb6-111">tooconfigure Azure AD integration with New Relic, you need hello following items:</span></span>

- <span data-ttu-id="d4fb6-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d4fb6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d4fb6-113">Uma assinatura habilitada para logon único do New Relic</span><span class="sxs-lookup"><span data-stu-id="d4fb6-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d4fb6-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d4fb6-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d4fb6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d4fb6-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d4fb6-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d4fb6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d4fb6-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d4fb6-118">Scenario description</span></span>
<span data-ttu-id="d4fb6-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d4fb6-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="d4fb6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d4fb6-121">Adicionando o New Relic na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d4fb6-121">Adding New Relic from hello gallery</span></span>
2. <span data-ttu-id="d4fb6-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d4fb6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-hello-gallery"></a><span data-ttu-id="d4fb6-123">Adicionando o New Relic na Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d4fb6-123">Adding New Relic from hello gallery</span></span>
<span data-ttu-id="d4fb6-124">integração de saudação tooconfigure do New Relic no AD do Azure, você precisa tooadd New Relic na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-124">tooconfigure hello integration of New Relic into Azure AD, you need tooadd New Relic from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d4fb6-125">**tooadd New Relic na Galeria de hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d4fb6-125">**tooadd New Relic from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d4fb6-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d4fb6-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d4fb6-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="d4fb6-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="d4fb6-133">Na caixa de pesquisa hello, digite **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-133">In hello search box, type **New Relic**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="d4fb6-135">No painel de resultados de saudação, selecione **New Relic**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-135">In hello results panel, select **New Relic**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d4fb6-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d4fb6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d4fb6-138">Nesta seção, você configurará e testará o logon único do Azure AD com o New Relic, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d4fb6-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no New Relic é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in New Relic is tooa user in Azure AD.</span></span> <span data-ttu-id="d4fb6-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no New Relic precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-140">In other words, a link relationship between an Azure AD user and hello related user in New Relic needs toobe established.</span></span>

<span data-ttu-id="d4fb6-141">No New Relic, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-141">In New Relic, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d4fb6-142">tooconfigure e teste de logon único do AD do Azure com o New Relic, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4fb6-142">tooconfigure and test Azure AD single sign-on with New Relic, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d4fb6-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d4fb6-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d4fb6-145">**[Criar um usuário de teste do New Relic](#creating-a-new-relic-test-user)**  -toohave um equivalente do Britta Simon no New Relic é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - toohave a counterpart of Britta Simon in New Relic that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d4fb6-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d4fb6-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d4fb6-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4fb6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d4fb6-149">Nesta seção, você habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo New Relic.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="d4fb6-150">**tooconfigure AD do Azure-logon único com o New Relic, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d4fb6-150">**tooconfigure Azure AD single sign-on with New Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="d4fb6-151">Em Olá portal do Azure, Olá **New Relic** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-151">In hello Azure portal, on hello **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="d4fb6-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="d4fb6-155">Em Olá **novo domínio Relic e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4fb6-155">On hello **New Relic Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="d4fb6-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="d4fb6-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d4fb6-158">Olá valor não é real.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-158">hello value is not real.</span></span> <span data-ttu-id="d4fb6-159">Valor de saudação de atualização com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="d4fb6-160">Entre em contato com [equipe de suporte do novo cliente Relic](https://support.newrelic.com/) tooget valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-160">Contact [New Relic Client support team](https://support.newrelic.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="d4fb6-161">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="d4fb6-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d4fb6-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d4fb6-165">Em Olá **nova configuração Relic** seção, clique em **configurar New Relic** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-165">On hello **New Relic Configuration** section, click **Configure New Relic** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d4fb6-166">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="d4fb6-166">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="d4fb6-168">Em uma janela de navegador web diferente, logon tooyour **New Relic** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-168">In a different web browser window, sign on tooyour **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="d4fb6-169">No menu de saudação na parte superior de saudação, clique em **configurações de conta**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-169">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="d4fb6-170">![Configurações de Conta](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Configurações de Conta")</span><span class="sxs-lookup"><span data-stu-id="d4fb6-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="d4fb6-171">Clique em Olá **autenticação e segurança** guia e, em seguida, clique em Olá **logon único** guia.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-171">Click hello **Security and authentication** tab, and then click hello **Single sign on** tab.</span></span>
   
    <span data-ttu-id="d4fb6-172">![Logon Único](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="d4fb6-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="d4fb6-173">Na página de diálogo SAML hello, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4fb6-173">On hello SAML dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="d4fb6-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="d4fb6-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="d4fb6-175">a.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-175">a.</span></span> <span data-ttu-id="d4fb6-176">Clique em **Escolher arquivo** tooupload seu certificado baixado do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-176">Click **Choose File** tooupload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="d4fb6-177">b.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-177">b.</span></span> <span data-ttu-id="d4fb6-178">Em Olá **URL de logon remoto** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-178">In hello **Remote login URL** textbox,  paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="d4fb6-179">c.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-179">c.</span></span> <span data-ttu-id="d4fb6-180">Em Olá **inicial da URL de Logout** caixa de texto valor Olá colar **URL de logout**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-180">In hello **Logout landing URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="d4fb6-181">d.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-181">d.</span></span> <span data-ttu-id="d4fb6-182">Clique em **Salvar minhas alterações**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="d4fb6-183">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="d4fb6-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d4fb6-184">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d4fb6-185">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d4fb6-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d4fb6-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d4fb6-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="d4fb6-187">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="d4fb6-189">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d4fb6-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d4fb6-190">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d4fb6-192">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d4fb6-194">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d4fb6-196">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4fb6-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d4fb6-198">a.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-198">a.</span></span> <span data-ttu-id="d4fb6-199">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d4fb6-200">b.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-200">b.</span></span> <span data-ttu-id="d4fb6-201">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d4fb6-202">c.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-202">c.</span></span> <span data-ttu-id="d4fb6-203">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d4fb6-204">d.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-204">d.</span></span> <span data-ttu-id="d4fb6-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="d4fb6-206">Criar um usuário de teste do New Relic</span><span class="sxs-lookup"><span data-stu-id="d4fb6-206">Creating a New Relic test user</span></span>

<span data-ttu-id="d4fb6-207">Em ordem tooenable Active Directory do Azure usuários toolog em tooNew Relic, eles devem ser provisionados no New Relic.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-207">In order tooenable Azure Active Directory users toolog in tooNew Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="d4fb6-208">No caso de saudação do New Relic, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-208">In hello case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="d4fb6-209">**tooprovision uma conta de usuário tooNew Relic, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d4fb6-209">**tooprovision a user account tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="d4fb6-210">Faça logon no tooyour **New Relic** site da empresa como administrador.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-210">Log in tooyour **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="d4fb6-211">No menu de saudação na parte superior de saudação, clique em **configurações de conta**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-211">In hello menu on hello top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="d4fb6-212">![Configurações de Conta](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Configurações de Conta")</span><span class="sxs-lookup"><span data-stu-id="d4fb6-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="d4fb6-213">Em Olá **conta** lado esquerdo do painel hello, clique em **resumo**e, em seguida, clique em **adicionar usuário**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-213">In hello **Account** pane on hello left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="d4fb6-214">![Configurações de Conta](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Configurações de Conta")</span><span class="sxs-lookup"><span data-stu-id="d4fb6-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="d4fb6-215">Em Olá **usuários ativos** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d4fb6-215">On hello **Active users** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="d4fb6-216">![Usuários ativos](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Usuários ativos")</span><span class="sxs-lookup"><span data-stu-id="d4fb6-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="d4fb6-217">a.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-217">a.</span></span> <span data-ttu-id="d4fb6-218">Em Olá **Email** caixa de texto, Olá tipo endereço de email de um usuário válido do Active Directory do Azure você deseja tooprovision.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-218">In hello **Email** textbox, type hello email address of a valid Azure Active Directory user you want tooprovision.</span></span>

    <span data-ttu-id="d4fb6-219">b.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-219">b.</span></span> <span data-ttu-id="d4fb6-220">Como **Função**, selecione **Usuário**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="d4fb6-221">c.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-221">c.</span></span> <span data-ttu-id="d4fb6-222">Clique em **Adicionar este usuário**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="d4fb6-223">Você pode usar qualquer ferramenta de criação outros New Relic usuário conta ou APIs fornecidas pelo New Relic tooprovision contas de usuário do AAD.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-223">You can use any other New Relic user account creation tools or APIs provided by New Relic tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d4fb6-224">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d4fb6-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d4fb6-225">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooNew Relic.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNew Relic.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="d4fb6-227">**tooassign tooNew Britta Simon Relic, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d4fb6-227">**tooassign Britta Simon tooNew Relic, perform hello following steps:**</span></span>

1. <span data-ttu-id="d4fb6-228">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d4fb6-230">Na lista de aplicativos hello, selecione **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-230">In hello applications list, select **New Relic**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="d4fb6-232">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="d4fb6-234">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-234">Click **Add** button.</span></span> <span data-ttu-id="d4fb6-235">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="d4fb6-237">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d4fb6-238">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d4fb6-239">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d4fb6-240">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="d4fb6-240">Testing single sign-on</span></span>

<span data-ttu-id="d4fb6-241">Olá o objetivo desta seção é tootest sua configuração de logon único do AD do Azure usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-241">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d4fb6-242">Quando você clica em bloco New Relic Olá Olá painel de acesso, você deve obter o aplicativo do New Relic tooyour automaticamente conectado em.</span><span class="sxs-lookup"><span data-stu-id="d4fb6-242">When you click hello New Relic tile in hello Access Panel, you should get automatically signed-on tooyour New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d4fb6-243">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d4fb6-243">Additional resources</span></span>

* [<span data-ttu-id="d4fb6-244">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d4fb6-244">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d4fb6-245">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d4fb6-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

