---
title: "Tutorial: Integração do Azure Active Directory om o InsideView | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o InsideView."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 979c0c24f3a18a193616061b8c2e78292233a56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="d5bbc-103">Tutorial: Integração do Active Directory do Azure com o InsideView</span><span class="sxs-lookup"><span data-stu-id="d5bbc-103">Tutorial: Azure Active Directory integration with InsideView</span></span>

<span data-ttu-id="d5bbc-104">Neste tutorial, você aprenderá como toointegrate InsideView com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="d5bbc-104">In this tutorial, you learn how toointegrate InsideView with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d5bbc-105">Integrando o InsideView com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5bbc-105">Integrating InsideView with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d5bbc-106">Você pode controlar no AD do Azure que tenha acesso tooInsideView</span><span class="sxs-lookup"><span data-stu-id="d5bbc-106">You can control in Azure AD who has access tooInsideView</span></span>
- <span data-ttu-id="d5bbc-107">Você pode habilitar seu usuários tooautomatically get conectado tooInsideView (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5bbc-107">You can enable your users tooautomatically get signed-on tooInsideView (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d5bbc-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d5bbc-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d5bbc-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d5bbc-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5bbc-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d5bbc-110">Prerequisites</span></span>

<span data-ttu-id="d5bbc-111">tooconfigure integração do AD do Azure com o InsideView, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5bbc-111">tooconfigure Azure AD integration with InsideView, you need hello following items:</span></span>

- <span data-ttu-id="d5bbc-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5bbc-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d5bbc-113">Uma assinatura habilitada para logon único do InsideView</span><span class="sxs-lookup"><span data-stu-id="d5bbc-113">A InsideView single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d5bbc-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d5bbc-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d5bbc-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d5bbc-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d5bbc-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d5bbc-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d5bbc-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d5bbc-118">Scenario description</span></span>
<span data-ttu-id="d5bbc-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d5bbc-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="d5bbc-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d5bbc-121">Adicionando InsideView da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d5bbc-121">Adding InsideView from hello gallery</span></span>
2. <span data-ttu-id="d5bbc-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5bbc-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insideview-from-hello-gallery"></a><span data-ttu-id="d5bbc-123">Adicionando InsideView da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d5bbc-123">Adding InsideView from hello gallery</span></span>
<span data-ttu-id="d5bbc-124">tooconfigure Olá integração da InsideView tooAzure AD, é necessário tooadd InsideView da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-124">tooconfigure hello integration of InsideView in tooAzure AD, you need tooadd InsideView from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d5bbc-125">**tooadd InsideView da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d5bbc-125">**tooadd InsideView from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5bbc-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d5bbc-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d5bbc-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="d5bbc-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="d5bbc-133">Na caixa de pesquisa hello, digite **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-133">In hello search box, type **InsideView**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. <span data-ttu-id="d5bbc-135">No painel de resultados de saudação, selecione **InsideView**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-135">In hello results panel, select **InsideView**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d5bbc-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5bbc-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d5bbc-138">Nesta seção, você configurará e testará o logon único do Azure AD com o InsideView, com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="d5bbc-138">In this section, you configure and test Azure AD single sign-on with InsideView based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d5bbc-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no InsideView é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in InsideView is tooa user in Azure AD.</span></span> <span data-ttu-id="d5bbc-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no InsideView precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-140">In other words, a link relationship between an Azure AD user and hello related user in InsideView needs toobe established.</span></span>

<span data-ttu-id="d5bbc-141">No InsideView, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-141">In InsideView, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d5bbc-142">tooconfigure e teste de logon único do AD do Azure com o InsideView, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5bbc-142">tooconfigure and test Azure AD single sign-on with InsideView, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d5bbc-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d5bbc-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d5bbc-145">**[Criar um usuário de teste do InsideView](#creating-a-insideview-test-user)**  -toohave um equivalente do Britta Simon no InsideView é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-145">**[Creating a InsideView test user](#creating-a-insideview-test-user)** - toohave a counterpart of Britta Simon in InsideView that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d5bbc-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d5bbc-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d5bbc-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d5bbc-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d5bbc-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo InsideView.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your InsideView application.</span></span>

<span data-ttu-id="d5bbc-150">**tooconfigure AD do Azure-logon único com o InsideView, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d5bbc-150">**tooconfigure Azure AD single sign-on with InsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5bbc-151">Em Olá portal do Azure, Olá **InsideView** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-151">In hello Azure portal, on hello **InsideView** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="d5bbc-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. <span data-ttu-id="d5bbc-155">Em Olá **InsideView domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5bbc-155">On hello **InsideView Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    <span data-ttu-id="d5bbc-157">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://my.insideview.com/iv/<STS Name>/login.iv`</span><span class="sxs-lookup"><span data-stu-id="d5bbc-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://my.insideview.com/iv/<STS Name>/login.iv`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d5bbc-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-158">This value is not real.</span></span> <span data-ttu-id="d5bbc-159">Atualize esse valor com hello URL de resposta real.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-159">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="d5bbc-160">Entre em contato com [InsideView a equipe de suporte ](mailto:support@insideview.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-160">Contact [InsideView support team ](mailto:support@insideview.com) tooget this value.</span></span>
 
4. <span data-ttu-id="d5bbc-161">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Raw)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-161">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. <span data-ttu-id="d5bbc-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d5bbc-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d5bbc-165">Em Olá **InsideView configuração** seção, clique em **configurar InsideView** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-165">On hello **InsideView Configuration** section, click **Configure InsideView** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d5bbc-166">Saudação de cópia **Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="d5bbc-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. <span data-ttu-id="d5bbc-168">Em uma janela de navegador web diferente, faça logon no site da empresa InsideView tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-168">In a different web browser window, log in tooyour InsideView company site as an administrator.</span></span>

8. <span data-ttu-id="d5bbc-169">Na barra de ferramentas de saudação na parte superior do hello, clique em **Admin**, **configurações de logon único**e, em seguida, clique em **adicionar SAML**.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-169">In hello toolbar on hello top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="d5bbc-170">![Configurações de Logon Único do SAML](./media/active-directory-saas-insideview-tutorial/ic794135.png "Configurações de Logon Único do SAML")</span><span class="sxs-lookup"><span data-stu-id="d5bbc-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span></span>

9. <span data-ttu-id="d5bbc-171">Em Olá **adicionar um novo SAML** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5bbc-171">In hello **Add a New SAML** section, perform hello following steps:</span></span>

    <span data-ttu-id="d5bbc-172">![Adicionar um Novo SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Adicionar um Novo SAML")</span><span class="sxs-lookup"><span data-stu-id="d5bbc-172">![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")</span></span>
   
    <span data-ttu-id="d5bbc-173">a.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-173">a.</span></span> <span data-ttu-id="d5bbc-174">Em Olá **STS Name** caixa de texto, digite um nome para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-174">In hello **STS Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="d5bbc-175">b.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-175">b.</span></span> <span data-ttu-id="d5bbc-176">Em **SamlP/WS-Fed ponto de extremidade não solicitadas** caixa de texto valor Olá colar **Single Sign-On URL do serviço SAML**, que você copiou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-176">In **SamlP/WS-Fed Unsolicited EndPoint** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="d5bbc-177">c.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-177">c.</span></span> <span data-ttu-id="d5bbc-178">Abra seu certificado codificado em base 64, que você baixou do Azure portal, Olá de copiar conteúdo dele para sua área de transferência, e, em seguida, cole-o toohello **Certificate STS** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-178">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **STS Certificate** textbox.</span></span>

    <span data-ttu-id="d5bbc-179">d.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-179">d.</span></span> <span data-ttu-id="d5bbc-180">Em Olá **mapeamento de Id de usuário do Crm** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-180">In hello **Crm User Id Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
        
    <span data-ttu-id="d5bbc-181">e.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-181">e.</span></span> <span data-ttu-id="d5bbc-182">Em Olá **Crm Email mapeamento** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-182">In hello **Crm Email Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="d5bbc-183">f.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-183">f.</span></span> <span data-ttu-id="d5bbc-184">Em Olá **Crm mapeamento** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-184">In hello **Crm First Name Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="d5bbc-185">g.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-185">g.</span></span> <span data-ttu-id="d5bbc-186">Em Olá **sobrenome do Crm mapeamento** caixa de texto, tipo `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-186">In hello **Crm lastName Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>  

    <span data-ttu-id="d5bbc-187">h.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-187">h.</span></span> <span data-ttu-id="d5bbc-188">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d5bbc-189">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="d5bbc-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d5bbc-190">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d5bbc-191">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d5bbc-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d5bbc-192">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5bbc-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="d5bbc-193">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="d5bbc-195">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d5bbc-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5bbc-196">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d5bbc-198">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d5bbc-200">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d5bbc-202">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5bbc-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d5bbc-204">a.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-204">a.</span></span> <span data-ttu-id="d5bbc-205">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d5bbc-206">b.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-206">b.</span></span> <span data-ttu-id="d5bbc-207">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d5bbc-208">c.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-208">c.</span></span> <span data-ttu-id="d5bbc-209">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d5bbc-210">d.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-210">d.</span></span> <span data-ttu-id="d5bbc-211">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-211">Click **Create**.</span></span>
 
### <a name="creating-a-insideview-test-user"></a><span data-ttu-id="d5bbc-212">Criação de um usuário de teste do InsideView</span><span class="sxs-lookup"><span data-stu-id="d5bbc-212">Creating a InsideView test user</span></span>

<span data-ttu-id="d5bbc-213">tooenable AD do Azure usuários toolog em tooInsideView, eles devem ser provisionados no tooInsideView.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-213">tooenable Azure AD users toolog in tooInsideView, they must be provisioned in tooInsideView.</span></span> <span data-ttu-id="d5bbc-214">No caso de saudação do InsideView, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-214">In hello case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="d5bbc-215">tooget usuários ou contatos criados no InsideView, entre em contato com [a equipe de suporte InsideView](mailto:support@insideview.com).</span><span class="sxs-lookup"><span data-stu-id="d5bbc-215">tooget users or contacts created in InsideView, Contact [InsideView support team](mailto:support@insideview.com).</span></span>

>[!NOTE]
><span data-ttu-id="d5bbc-216">Você pode usar qualquer ferramenta de criação outros InsideView usuário conta ou APIs fornecidas pela InsideView tooprovision contas de usuário do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-216">You can use any other InsideView user account creation tools or APIs provided by InsideView tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d5bbc-217">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d5bbc-217">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d5bbc-218">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooInsideView.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-218">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInsideView.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="d5bbc-220">**tooassign Britta Simon tooInsideView, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d5bbc-220">**tooassign Britta Simon tooInsideView, perform hello following steps:**</span></span>

1. <span data-ttu-id="d5bbc-221">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-221">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d5bbc-223">Na lista de aplicativos hello, selecione **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-223">In hello applications list, select **InsideView**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. <span data-ttu-id="d5bbc-225">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-225">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="d5bbc-227">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-227">Click **Add** button.</span></span> <span data-ttu-id="d5bbc-228">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="d5bbc-230">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-230">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d5bbc-231">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d5bbc-232">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d5bbc-233">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="d5bbc-233">Testing single sign-on</span></span>

<span data-ttu-id="d5bbc-234">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-234">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d5bbc-235">Quando você clica em bloco InsideView Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour InsideView aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d5bbc-235">When you click hello InsideView tile in hello Access Panel, you should get automatically signed-on tooyour InsideView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d5bbc-236">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d5bbc-236">Additional resources</span></span>

* [<span data-ttu-id="d5bbc-237">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d5bbc-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d5bbc-238">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d5bbc-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png

