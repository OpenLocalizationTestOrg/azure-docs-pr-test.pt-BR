---
title: "Tutorial: Integração do Azure Active Directory ao Samanage | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e do Samanage."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f0db4fb0-7eec-48c2-9c7a-beab1ab49bc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: c8edc29f113b8088438618a731e97c0f4f155b9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-samanage"></a><span data-ttu-id="ad0ef-103">Tutorial: Integração do Azure Active Directory ao Samanage</span><span class="sxs-lookup"><span data-stu-id="ad0ef-103">Tutorial: Azure Active Directory integration with Samanage</span></span>

<span data-ttu-id="ad0ef-104">Neste tutorial, você aprenderá como toointegrate Samanage com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="ad0ef-104">In this tutorial, you learn how toointegrate Samanage with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ad0ef-105">Integrando o Samanage com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="ad0ef-105">Integrating Samanage with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ad0ef-106">Você pode controlar no AD do Azure que tenha acesso tooSamanage</span><span class="sxs-lookup"><span data-stu-id="ad0ef-106">You can control in Azure AD who has access tooSamanage</span></span>
- <span data-ttu-id="ad0ef-107">Você pode habilitar seu usuários tooautomatically get conectado tooSamanage (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ad0ef-107">You can enable your users tooautomatically get signed-on tooSamanage (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ad0ef-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ad0ef-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ad0ef-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ad0ef-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad0ef-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ad0ef-110">Prerequisites</span></span>

<span data-ttu-id="ad0ef-111">tooconfigure integração do AD do Azure com o Samanage, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="ad0ef-111">tooconfigure Azure AD integration with Samanage, you need hello following items:</span></span>

- <span data-ttu-id="ad0ef-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ad0ef-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ad0ef-113">Uma assinatura habilitada para logon único do Samanage</span><span class="sxs-lookup"><span data-stu-id="ad0ef-113">A Samanage single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ad0ef-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ad0ef-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="ad0ef-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ad0ef-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ad0ef-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ad0ef-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ad0ef-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="ad0ef-118">Scenario description</span></span>
<span data-ttu-id="ad0ef-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ad0ef-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="ad0ef-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ad0ef-121">Adicionando Samanage da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ad0ef-121">Adding Samanage from hello gallery</span></span>
2. <span data-ttu-id="ad0ef-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ad0ef-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-samanage-from-hello-gallery"></a><span data-ttu-id="ad0ef-123">Adicionando Samanage da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="ad0ef-123">Adding Samanage from hello gallery</span></span>
<span data-ttu-id="ad0ef-124">integração de saudação tooconfigure do Samanage no AD do Azure, você precisa tooadd Samanage da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-124">tooconfigure hello integration of Samanage into Azure AD, you need tooadd Samanage from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ad0ef-125">**tooadd Samanage da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ad0ef-125">**tooadd Samanage from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad0ef-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ad0ef-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ad0ef-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="ad0ef-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="ad0ef-133">Na caixa de pesquisa hello, digite **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-133">In hello search box, type **Samanage**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_search.png)

5. <span data-ttu-id="ad0ef-135">No painel de resultados de saudação, selecione **Samanage**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-135">In hello results panel, select **Samanage**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ad0ef-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ad0ef-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ad0ef-138">Nesta seção, você configura e testa o logon único do Azure AD com o Samanage, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-138">In this section, you configure and test Azure AD single sign-on with Samanage based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ad0ef-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Samanage é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Samanage is tooa user in Azure AD.</span></span> <span data-ttu-id="ad0ef-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Samanage precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-140">In other words, a link relationship between an Azure AD user and hello related user in Samanage needs toobe established.</span></span>

<span data-ttu-id="ad0ef-141">No Samanage, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-141">In Samanage, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ad0ef-142">tooconfigure e teste de logon único do AD do Azure com o Samanage, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="ad0ef-142">tooconfigure and test Azure AD single sign-on with Samanage, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ad0ef-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ad0ef-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ad0ef-145">**[Criar um usuário de teste do Samanage](#creating-a-samanage-test-user)**  -toohave um equivalente do Britta Simon no Samanage é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-145">**[Creating a Samanage test user](#creating-a-samanage-test-user)** - toohave a counterpart of Britta Simon in Samanage that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ad0ef-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ad0ef-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ad0ef-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="ad0ef-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ad0ef-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Samanage.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Samanage application.</span></span>

<span data-ttu-id="ad0ef-150">**tooconfigure AD do Azure-logon único com o Samanage, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ad0ef-150">**tooconfigure Azure AD single sign-on with Samanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad0ef-151">Em Olá portal do Azure, Olá **Samanage** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-151">In hello Azure portal, on hello **Samanage** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="ad0ef-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_samlbase.png)

3. <span data-ttu-id="ad0ef-155">Em Olá **Samanage domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ad0ef-155">On hello **Samanage Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_url.png)

    <span data-ttu-id="ad0ef-157">a.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-157">a.</span></span> <span data-ttu-id="ad0ef-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<Company Name>.samanage.com/saml_login/<Company Name>`</span><span class="sxs-lookup"><span data-stu-id="ad0ef-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com/saml_login/<Company Name>`</span></span>

    <span data-ttu-id="ad0ef-159">b.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-159">b.</span></span> <span data-ttu-id="ad0ef-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<Company Name>.samanage.com`</span><span class="sxs-lookup"><span data-stu-id="ad0ef-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<Company Name>.samanage.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ad0ef-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-161">These values are not real.</span></span> <span data-ttu-id="ad0ef-162">Atualize esses valores com URL de logon real hello e o identificador que é explicada posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-162">Update these values with hello actual Sign-on URL and Identifier, which is explained later in hello tutorial.</span></span> <span data-ttu-id="ad0ef-163">Para obter mais detalhes, contate a [equipe de suporte ao Cliente do Samanage](https://www.samanage.com/support).</span><span class="sxs-lookup"><span data-stu-id="ad0ef-163">For more details contact [Samanage Client support team](https://www.samanage.com/support).</span></span>    
 
4. <span data-ttu-id="ad0ef-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_certificate.png) 

5. <span data-ttu-id="ad0ef-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="ad0ef-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ad0ef-168">Em Olá **Samanage configuração** seção, clique em **configurar Samanage** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-168">On hello **Samanage Configuration** section, click **Configure Samanage** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ad0ef-169">Saudação de cópia **URL de logout e a ID da entidade SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="ad0ef-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_configure.png) 

7. <span data-ttu-id="ad0ef-171">Em uma janela diferente do navegador da Web, faça logon no site da sua empresa do Samanage como administrador.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-171">In a different web browser window, log into your Samanage company site as an administrator.</span></span>

8. <span data-ttu-id="ad0ef-172">Clique em **Painel** e selecione **Configuração** no painel de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-172">Click **Dashboard** and select **Setup** in left navigation pane.</span></span>
   
    <span data-ttu-id="ad0ef-173">![Painel](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Painel")</span><span class="sxs-lookup"><span data-stu-id="ad0ef-173">![Dashboard](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Dashboard")</span></span>

9. <span data-ttu-id="ad0ef-174">Clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-174">Click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="ad0ef-175">![Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="ad0ef-175">![Single Sign-On](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_002.png "Single Sign-On")</span></span>

10. <span data-ttu-id="ad0ef-176">Navegue muito**logon usando SAML** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ad0ef-176">Navigate too**Login using SAML** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ad0ef-177">![Logon usando SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Logon usando SAML")</span><span class="sxs-lookup"><span data-stu-id="ad0ef-177">![Login using SAML](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_003.png "Login using SAML")</span></span>
 
    <span data-ttu-id="ad0ef-178">a.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-178">a.</span></span> <span data-ttu-id="ad0ef-179">Clique em **Habilitar o Logon Único com SAML**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-179">Click **Enable Single Sign-On with SAML**.</span></span>  
 
    <span data-ttu-id="ad0ef-180">b.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-180">b.</span></span> <span data-ttu-id="ad0ef-181">Em hello **URL do provedor de identidade** caixa de texto valor Olá colar **ID da entidade SAML** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-181">In hello **Identity Provider URL** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>    
 
    <span data-ttu-id="ad0ef-182">c.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-182">c.</span></span> <span data-ttu-id="ad0ef-183">Confirmar Olá **URL de logon** correspondências Olá **URL de logon** de **Samanage domínio e URLs** seção no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-183">Confirm hello **Login URL** matches hello **Sign On URL** of **Samanage Domain and URLs** section in Azure portal.</span></span>
 
    <span data-ttu-id="ad0ef-184">d.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-184">d.</span></span> <span data-ttu-id="ad0ef-185">Em Olá **URL de Logout** caixa de texto, insira o valor de saudação do **URL de logout** que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-185">In hello **Logout URL** textbox, enter hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="ad0ef-186">e.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-186">e.</span></span> <span data-ttu-id="ad0ef-187">Em Olá **emissor SAML** caixa de texto, a id do tipo de aplicativo hello URI definido no seu provedor de identidade.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-187">In hello **SAML Issuer** textbox, type hello app id URI set in your identity provider.</span></span>
 
    <span data-ttu-id="ad0ef-188">f.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-188">f.</span></span> <span data-ttu-id="ad0ef-189">Abra seu certificado codificado em base 64 baixado do portal do Azure no bloco de notas, Olá de copiar conteúdo dele para sua área de transferência e, em seguida, cole-o toohello **cole seu provedor de identidade x. 509 certificado abaixo** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-189">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **Paste your Identity Provider x.509 Certificate below** textbox.</span></span>
 
    <span data-ttu-id="ad0ef-190">g.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-190">g.</span></span> <span data-ttu-id="ad0ef-191">Clique em **Criar usuários se eles não existirem no Samanage**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-191">Click **Create users if they do not exist in Samanage**.</span></span>
 
    <span data-ttu-id="ad0ef-192">h.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-192">h.</span></span> <span data-ttu-id="ad0ef-193">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-193">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="ad0ef-194">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="ad0ef-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ad0ef-195">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ad0ef-196">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ad0ef-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ad0ef-197">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ad0ef-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="ad0ef-198">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="ad0ef-200">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ad0ef-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad0ef-201">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ad0ef-203">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ad0ef-205">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ad0ef-207">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ad0ef-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-samanage-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ad0ef-209">a.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-209">a.</span></span> <span data-ttu-id="ad0ef-210">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ad0ef-211">b.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-211">b.</span></span> <span data-ttu-id="ad0ef-212">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ad0ef-213">c.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-213">c.</span></span> <span data-ttu-id="ad0ef-214">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ad0ef-215">d.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-215">d.</span></span> <span data-ttu-id="ad0ef-216">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-216">Click **Create**.</span></span>
 
### <a name="creating-a-samanage-test-user"></a><span data-ttu-id="ad0ef-217">Criação de um usuário de teste de Samanage</span><span class="sxs-lookup"><span data-stu-id="ad0ef-217">Creating a Samanage test user</span></span>

<span data-ttu-id="ad0ef-218">tooenable AD do Azure usuários toolog em tooSamanage, eles devem ser provisionados no Samanage.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-218">tooenable Azure AD users toolog in tooSamanage, they must be provisioned into Samanage.</span></span>  
<span data-ttu-id="ad0ef-219">No caso de saudação do Samanage, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-219">In hello case of Samanage, provisioning is a manual task.</span></span>

<span data-ttu-id="ad0ef-220">**tooprovision uma conta de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ad0ef-220">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad0ef-221">Faça logon em seu site de empresa Samanage como um administrador.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-221">Log into your Samanage company site as an administrator.</span></span>

2. <span data-ttu-id="ad0ef-222">Clique em **Painel** e selecione **Configuração** no painel de navegação à esquerda.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-222">Click **Dashboard** and select **Setup** in left navigation pan.</span></span>
   
    <span data-ttu-id="ad0ef-223">![Configuração](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Configuração")</span><span class="sxs-lookup"><span data-stu-id="ad0ef-223">![Setup](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_001.png "Setup")</span></span>

3. <span data-ttu-id="ad0ef-224">Clique em Olá **usuários** guia</span><span class="sxs-lookup"><span data-stu-id="ad0ef-224">Click hello **Users** tab</span></span>
   
    <span data-ttu-id="ad0ef-225">![Usuários](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Usuários")</span><span class="sxs-lookup"><span data-stu-id="ad0ef-225">![Users](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_006.png "Users")</span></span>

4. <span data-ttu-id="ad0ef-226">Clique em **Novo Usuário**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-226">Click **New User**.</span></span>
   
    <span data-ttu-id="ad0ef-227">![Novo Usuário](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "Novo Usuário")</span><span class="sxs-lookup"><span data-stu-id="ad0ef-227">![New User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_007.png "New User")</span></span>

5. <span data-ttu-id="ad0ef-228">Saudação de tipo **nome** e hello **endereço de Email** de uma conta do Active Directory do Azure que deseja tooprovision e clique **criar usuário**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-228">Type hello **Name** and hello **Email Address** of an Azure Active Directory account you want tooprovision and click **Create user**.</span></span>
   
    <span data-ttu-id="ad0ef-229">![Criar usuário](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Criar usuário")</span><span class="sxs-lookup"><span data-stu-id="ad0ef-229">![Create User](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_008.png "Create User")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="ad0ef-230">proprietário de conta do Active Directory do Azure Olá será receberá um email e execute tooconfirm um link em sua conta antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-230">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="ad0ef-231">Você pode usar qualquer ferramenta de criação outros Samanage usuário conta ou APIs fornecidas pelo Samanage tooprovision Azure Active Directory as contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-231">You can use any other Samanage user account creation tools or APIs provided by Samanage tooprovision Azure Active Directory user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ad0ef-232">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="ad0ef-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ad0ef-233">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooSamanage.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSamanage.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="ad0ef-235">**tooassign Britta Simon tooSamanage, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="ad0ef-235">**tooassign Britta Simon tooSamanage, perform hello following steps:**</span></span>

1. <span data-ttu-id="ad0ef-236">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="ad0ef-238">Na lista de aplicativos hello, selecione **Samanage**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-238">In hello applications list, select **Samanage**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-samanage-tutorial/tutorial_samanage_app.png) 

3. <span data-ttu-id="ad0ef-240">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="ad0ef-242">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-242">Click **Add** button.</span></span> <span data-ttu-id="ad0ef-243">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="ad0ef-245">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ad0ef-246">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ad0ef-247">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ad0ef-248">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="ad0ef-248">Testing single sign-on</span></span>

<span data-ttu-id="ad0ef-249">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ad0ef-250">Quando você clica em bloco Samanage Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Samanage aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ad0ef-250">When you click hello Samanage tile in hello Access Panel, you should get automatically signed-on tooyour Samanage application.</span></span>
<span data-ttu-id="ad0ef-251">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ad0ef-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ad0ef-252">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="ad0ef-252">Additional resources</span></span>

* [<span data-ttu-id="ad0ef-253">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ad0ef-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ad0ef-254">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ad0ef-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samanage-tutorial/tutorial_general_203.png

