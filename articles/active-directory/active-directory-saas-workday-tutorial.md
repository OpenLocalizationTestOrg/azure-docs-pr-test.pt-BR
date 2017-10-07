---
title: "Tutorial: integração do Azure Active Directory com o Workday | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Workday."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e9da692e-4a65-4231-8ab3-bc9a87b10bca
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: aaa41e372e45f464c4540a70fc79c98dbc06d6b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workday"></a><span data-ttu-id="3d15f-103">Tutorial: Integração do Active Directory do Azure com o Workday</span><span class="sxs-lookup"><span data-stu-id="3d15f-103">Tutorial: Azure Active Directory integration with Workday</span></span>

<span data-ttu-id="3d15f-104">Neste tutorial, você aprenderá como toointegrate dia de trabalho com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="3d15f-104">In this tutorial, you learn how toointegrate Workday with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3d15f-105">Integrando o Workday com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d15f-105">Integrating Workday with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="3d15f-106">Você pode controlar no AD do Azure que tenha acesso tooWorkday</span><span class="sxs-lookup"><span data-stu-id="3d15f-106">You can control in Azure AD who has access tooWorkday</span></span>
- <span data-ttu-id="3d15f-107">Você pode habilitar seu usuários tooautomatically get conectado tooWorkday (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3d15f-107">You can enable your users tooautomatically get signed-on tooWorkday (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3d15f-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="3d15f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="3d15f-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d15f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d15f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3d15f-110">Prerequisites</span></span>

<span data-ttu-id="3d15f-111">tooconfigure integração do AD do Azure com o Workday, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d15f-111">tooconfigure Azure AD integration with Workday, you need hello following items:</span></span>

- <span data-ttu-id="3d15f-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3d15f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d15f-113">Uma assinatura do Workday habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="3d15f-113">A Workday single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3d15f-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3d15f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3d15f-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="3d15f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d15f-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="3d15f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3d15f-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d15f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d15f-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="3d15f-118">Scenario description</span></span>
<span data-ttu-id="3d15f-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="3d15f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3d15f-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="3d15f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d15f-121">Adicionando Workday da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3d15f-121">Adding Workday from hello gallery</span></span>
2. <span data-ttu-id="3d15f-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3d15f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workday-from-hello-gallery"></a><span data-ttu-id="3d15f-123">Adicionando Workday da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="3d15f-123">Adding Workday from hello gallery</span></span>
<span data-ttu-id="3d15f-124">tooconfigure Olá integração da Workday AD do Azure, você precisa tooadd Workday na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="3d15f-124">tooconfigure hello integration of Workday into Azure AD, you need tooadd Workday from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="3d15f-125">**tooadd Workday da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3d15f-125">**tooadd Workday from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d15f-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3d15f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3d15f-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="3d15f-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="3d15f-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3d15f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="3d15f-133">Na caixa de pesquisa hello, digite **Workday**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-133">In hello search box, type **Workday**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/tutorial_workday_search.png)

5. <span data-ttu-id="3d15f-135">No painel de resultados de saudação, selecione **Workday**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="3d15f-135">In hello results panel, select **Workday**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/tutorial_workday_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3d15f-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3d15f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3d15f-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Workday com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="3d15f-138">In this section, you configure and test Azure AD single sign-on with Workday based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3d15f-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Workday é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d15f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workday is tooa user in Azure AD.</span></span> <span data-ttu-id="3d15f-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Workday precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="3d15f-140">In other words, a link relationship between an Azure AD user and hello related user in Workday needs toobe established.</span></span>

<span data-ttu-id="3d15f-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no Workday.</span><span class="sxs-lookup"><span data-stu-id="3d15f-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Workday.</span></span>

<span data-ttu-id="3d15f-142">tooconfigure e teste de logon único do AD do Azure com o Workday, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d15f-142">tooconfigure and test Azure AD single sign-on with Workday, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="3d15f-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="3d15f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="3d15f-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d15f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d15f-145">**[Criar um usuário de teste Workday](#creating-a-workday-test-user)**  -toohave um equivalente do Britta Simon no Workday é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="3d15f-145">**[Creating a Workday test user](#creating-a-workday-test-user)** - toohave a counterpart of Britta Simon in Workday that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="3d15f-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="3d15f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d15f-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="3d15f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3d15f-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d15f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3d15f-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de dia de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3d15f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workday application.</span></span>

<span data-ttu-id="3d15f-150">**tooconfigure AD do Azure-logon único com o Workday, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3d15f-150">**tooconfigure Azure AD single sign-on with Workday, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d15f-151">Em Olá portal do Azure, Olá **Workday** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-151">In hello Azure portal, on hello **Workday** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="3d15f-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="3d15f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_samlbase.png)

3. <span data-ttu-id="3d15f-155">Em Olá **domínio Workday e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d15f-155">On hello **Workday Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_url.png)

    <span data-ttu-id="3d15f-157">a.</span><span class="sxs-lookup"><span data-stu-id="3d15f-157">a.</span></span> <span data-ttu-id="3d15f-158">Em Olá **URL de logon** texto, o valor do tipo hello como:`https://impl.workday.com/<tenant>/login-saml2.htmld`</span><span class="sxs-lookup"><span data-stu-id="3d15f-158">In hello **Sign-on URL** textbox, type hello value as: `https://impl.workday.com/<tenant>/login-saml2.htmld`</span></span>

    <span data-ttu-id="3d15f-159">b.</span><span class="sxs-lookup"><span data-stu-id="3d15f-159">b.</span></span> <span data-ttu-id="3d15f-160">Em Olá **URL de resposta** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://impl.workday.com/<tenant>/login-saml.htmld`</span><span class="sxs-lookup"><span data-stu-id="3d15f-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://impl.workday.com/<tenant>/login-saml.htmld`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3d15f-161">Esses valores não são Olá real.</span><span class="sxs-lookup"><span data-stu-id="3d15f-161">These values are not hello real.</span></span> <span data-ttu-id="3d15f-162">Atualize esses valores com URL de logon real hello e a URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="3d15f-162">Update these values with hello actual Sign-on URL and Reply URL.</span></span> <span data-ttu-id="3d15f-163">Sua URL de resposta deve ter um subdomínio, por exemplo: www, wd2, wd3, wd3-impl, wd5, wd5-impl.</span><span class="sxs-lookup"><span data-stu-id="3d15f-163">Your reply URL must have a subdomain for example: www, wd2, wd3, wd3-impl, wd5, wd5-impl).</span></span> <span data-ttu-id="3d15f-164">O uso de algo como "*http://www.myworkday.com*" funciona, mas "*http://myworkday.com*", não.</span><span class="sxs-lookup"><span data-stu-id="3d15f-164">Using something like "*http://www.myworkday.com*" works but "*http://myworkday.com*" does not.</span></span> <span data-ttu-id="3d15f-165">Entre em contato com [equipe de suporte do Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="3d15f-165">Contact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget these values.</span></span> 
 

4. <span data-ttu-id="3d15f-166">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3d15f-166">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_certificate.png) 

5. <span data-ttu-id="3d15f-168">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="3d15f-168">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3d15f-170">Em Olá **Workday configuração** seção, clique em **configurar Workday** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="3d15f-170">On hello **Workday Configuration** section, click **Configure Workday** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="3d15f-171">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="3d15f-171">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="3d15f-172">![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="3d15f-172">![Configure Single Sign-On](./media/active-directory-saas-workday-tutorial/tutorial_workday_configure.png) 
<CS></span></span>
7. <span data-ttu-id="3d15f-173">Em uma janela de navegador web diferente, faça logon no site da empresa tooyour Workday como um administrador.</span><span class="sxs-lookup"><span data-stu-id="3d15f-173">In a different web browser window, log in tooyour Workday company site as an administrator.</span></span>

8. <span data-ttu-id="3d15f-174">Vá muito**Menu \> Workbench**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-174">Go too**Menu \> Workbench**.</span></span>
   
    <span data-ttu-id="3d15f-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span><span class="sxs-lookup"><span data-stu-id="3d15f-175">![Workbench](./media/active-directory-saas-workday-tutorial/IC782923.png "Workbench")</span></span>

9. <span data-ttu-id="3d15f-176">Vá muito**administração da conta**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-176">Go too**Account Administration**.</span></span>
   
    <span data-ttu-id="3d15f-177">![Administração de Conta](./media/active-directory-saas-workday-tutorial/IC782924.png "Administração de Conta")</span><span class="sxs-lookup"><span data-stu-id="3d15f-177">![Account Administration](./media/active-directory-saas-workday-tutorial/IC782924.png "Account Administration")</span></span>

10. <span data-ttu-id="3d15f-178">Vá muito**Editar configuração de locatário – segurança**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-178">Go too**Edit Tenant Setup – Security**.</span></span>
   
    <span data-ttu-id="3d15f-179">![Editar segurança de locatário](./media/active-directory-saas-workday-tutorial/IC782925.png "Editar segurança de locatário")</span><span class="sxs-lookup"><span data-stu-id="3d15f-179">![Edit Tenant Security](./media/active-directory-saas-workday-tutorial/IC782925.png "Edit Tenant Security")</span></span>

11. <span data-ttu-id="3d15f-180">Em Olá **URLs de redirecionamento** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d15f-180">In hello **Redirection URLs** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="3d15f-181">![URLs de redirecionamento](./media/active-directory-saas-workday-tutorial/IC7829581.png "URLs de redirecionamento")</span><span class="sxs-lookup"><span data-stu-id="3d15f-181">![Redirection URLs](./media/active-directory-saas-workday-tutorial/IC7829581.png "Redirection URLs")</span></span>
   
    <span data-ttu-id="3d15f-182">a.</span><span class="sxs-lookup"><span data-stu-id="3d15f-182">a.</span></span> <span data-ttu-id="3d15f-183">Clique em **Adicionar Linha**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-183">Click **Add Row**.</span></span>
   
    <span data-ttu-id="3d15f-184">b.</span><span class="sxs-lookup"><span data-stu-id="3d15f-184">b.</span></span> <span data-ttu-id="3d15f-185">Em Olá **URL de redirecionamento de logon** caixa de texto e hello **URL de redirecionamento móvel** caixa de texto, Olá tipo **URL de logon** você inseriu Olá **Workday domínio e URLs** seção Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d15f-185">In hello **Login Redirect URL** textbox and hello **Mobile Redirect URL** textbox, type hello **Sign-on URL** you have entered on hello **Workday Domain and URLs** section of hello Azure portal.</span></span>
   
    <span data-ttu-id="3d15f-186">c.</span><span class="sxs-lookup"><span data-stu-id="3d15f-186">c.</span></span> <span data-ttu-id="3d15f-187">Em Olá portal do Azure, Olá **configurar o logon** janela, Olá cópia **URL de logout**e, em seguida, cole-Olá **URL de redirecionamento de Logout** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3d15f-187">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL**, and then paste it into hello **Logout Redirect URL** textbox.</span></span>
   
    <span data-ttu-id="3d15f-188">d.</span><span class="sxs-lookup"><span data-stu-id="3d15f-188">d.</span></span>  <span data-ttu-id="3d15f-189">Em **ambiente** caixa de texto Nome do tipo hello ambiente.</span><span class="sxs-lookup"><span data-stu-id="3d15f-189">In **Environment** textbox, type hello environment name.</span></span>  

    >[!NOTE]
    > <span data-ttu-id="3d15f-190">Olá valor do atributo de ambiente hello está ligado toohello valor saudação do URL de locatário:</span><span class="sxs-lookup"><span data-stu-id="3d15f-190">hello value of hello Environment attribute is tied toohello value of hello tenant URL:</span></span>  
    ><span data-ttu-id="3d15f-191">-Se nome de domínio de saudação do URL do locatário do Workday Olá começa com impl por exemplo: *https://impl.workday.com/\<locatário\>/login-saml2.htmld*), Olá **ambiente** atributo deve ser definido como tooImplementation.</span><span class="sxs-lookup"><span data-stu-id="3d15f-191">-If hello domain name of hello Workday tenant URL starts with impl for example: *https://impl.workday.com/\<tenant\>/login-saml2.htmld*), hello **Environment** attribute must be set tooImplementation.</span></span>  
    ><span data-ttu-id="3d15f-192">-Se o nome de domínio Olá começa com outra coisa, você precisa toocontact [equipe de suporte do Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html) tooget Olá correspondência **ambiente** valor.</span><span class="sxs-lookup"><span data-stu-id="3d15f-192">-If hello domain name starts with something else, you need toocontact [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) tooget hello matching **Environment** value.</span></span>

12. <span data-ttu-id="3d15f-193">Em Olá **instalação do SAML** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d15f-193">In hello **SAML Setup** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="3d15f-194">![Instalação do SAML](./media/active-directory-saas-workday-tutorial/IC782926.png "Instalação do SAML")</span><span class="sxs-lookup"><span data-stu-id="3d15f-194">![SAML Setup](./media/active-directory-saas-workday-tutorial/IC782926.png "SAML Setup")</span></span>
   
    <span data-ttu-id="3d15f-195">a.</span><span class="sxs-lookup"><span data-stu-id="3d15f-195">a.</span></span>  <span data-ttu-id="3d15f-196">Selecione **Habilitar Autenticação SAML**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-196">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="3d15f-197">b.</span><span class="sxs-lookup"><span data-stu-id="3d15f-197">b.</span></span>  <span data-ttu-id="3d15f-198">Clique em **Adicionar Linha**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-198">Click **Add Row**.</span></span>

13. <span data-ttu-id="3d15f-199">Olá seção provedores de identidade SAML, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d15f-199">In hello SAML Identity Providers section, perform hello following steps:</span></span>
   
    <span data-ttu-id="3d15f-200">![Provedores de Identidade SAML](./media/active-directory-saas-workday-tutorial/IC7829271.png "Provedores de Identidade SAML")</span><span class="sxs-lookup"><span data-stu-id="3d15f-200">![SAML Identity Providers](./media/active-directory-saas-workday-tutorial/IC7829271.png "SAML Identity Providers")</span></span>
   
    <span data-ttu-id="3d15f-201">a.</span><span class="sxs-lookup"><span data-stu-id="3d15f-201">a.</span></span> <span data-ttu-id="3d15f-202">Na caixa de texto de nome do provedor de identidade hello, digite um nome de provedor (por exemplo: *SPInitiatedSSO*).</span><span class="sxs-lookup"><span data-stu-id="3d15f-202">In hello Identity Provider Name textbox, type a provider name (for example: *SPInitiatedSSO*).</span></span>
   
    <span data-ttu-id="3d15f-203">b.</span><span class="sxs-lookup"><span data-stu-id="3d15f-203">b.</span></span> <span data-ttu-id="3d15f-204">Em Olá portal do Azure, Olá **configurar o logon** janela, Olá cópia **ID da entidade SAML** valor e, em seguida, cole-Olá **emissor** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3d15f-204">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Entity ID** value, and then paste it into hello **Issuer** textbox.</span></span>
   
    <span data-ttu-id="3d15f-205">c.</span><span class="sxs-lookup"><span data-stu-id="3d15f-205">c.</span></span> <span data-ttu-id="3d15f-206">Selecione **Habilitar Logoff Iniciado pelo Workday**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-206">Select **Enable Workday Initiated Logout**.</span></span>
   
    <span data-ttu-id="3d15f-207">d.</span><span class="sxs-lookup"><span data-stu-id="3d15f-207">d.</span></span> <span data-ttu-id="3d15f-208">Em Olá portal do Azure, Olá **configurar o logon** janela, Olá cópia **URL de logout** valor e, em seguida, cole-o em Olá **URL de solicitação de Logout** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3d15f-208">In hello Azure portal, on hello **Configure sign-on** window, copy hello **Sign-Out URL** value, and then paste it into hello **Logout Request URL** textbox.</span></span>

    <span data-ttu-id="3d15f-209">e.</span><span class="sxs-lookup"><span data-stu-id="3d15f-209">e.</span></span> <span data-ttu-id="3d15f-210">Clique em **Certificado de Chave Pública do Provedor de Identidade** e em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-210">Click **Identity Provider Public Key Certificate**, and then click **Create**.</span></span> 

    <span data-ttu-id="3d15f-211">![Criar](./media/active-directory-saas-workday-tutorial/IC782928.png "Criar")</span><span class="sxs-lookup"><span data-stu-id="3d15f-211">![Create](./media/active-directory-saas-workday-tutorial/IC782928.png "Create")</span></span>

    <span data-ttu-id="3d15f-212">f.</span><span class="sxs-lookup"><span data-stu-id="3d15f-212">f.</span></span> <span data-ttu-id="3d15f-213">Clique em **Criar Chave Pública x509**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-213">Click **Create x509 Public Key**.</span></span> 

    <span data-ttu-id="3d15f-214">![Criar](./media/active-directory-saas-workday-tutorial/IC782929.png "Criar")</span><span class="sxs-lookup"><span data-stu-id="3d15f-214">![Create](./media/active-directory-saas-workday-tutorial/IC782929.png "Create")</span></span>


14. <span data-ttu-id="3d15f-215">Em Olá **exibir chave pública x509** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d15f-215">In hello **View x509 Public Key** section, perform hello following steps:</span></span> 
   
    <span data-ttu-id="3d15f-216">![Exibir chave pública x509](./media/active-directory-saas-workday-tutorial/IC782930.png "Exibir chave pública x509")</span><span class="sxs-lookup"><span data-stu-id="3d15f-216">![View x509 Public Key](./media/active-directory-saas-workday-tutorial/IC782930.png "View x509 Public Key")</span></span> 
   
    <span data-ttu-id="3d15f-217">a.</span><span class="sxs-lookup"><span data-stu-id="3d15f-217">a.</span></span> <span data-ttu-id="3d15f-218">Em Olá **nome** caixa de texto, digite um nome para o certificado (por exemplo: *PPE\_SP*).</span><span class="sxs-lookup"><span data-stu-id="3d15f-218">In hello **Name** textbox, type a name for your certificate (for example: *PPE\_SP*).</span></span>
   
    <span data-ttu-id="3d15f-219">b.</span><span class="sxs-lookup"><span data-stu-id="3d15f-219">b.</span></span> <span data-ttu-id="3d15f-220">Em Olá **válido de** caixa de texto, Olá de tipo válido do valor de atributo do seu certificado.</span><span class="sxs-lookup"><span data-stu-id="3d15f-220">In hello **Valid From** textbox, type hello valid from attribute value of your certificate.</span></span>
   
    <span data-ttu-id="3d15f-221">c.</span><span class="sxs-lookup"><span data-stu-id="3d15f-221">c.</span></span>  <span data-ttu-id="3d15f-222">Em Olá **válido até** caixa de texto valor do tipo hello tooattribute válido do seu certificado.</span><span class="sxs-lookup"><span data-stu-id="3d15f-222">In hello **Valid To** textbox, type hello valid tooattribute value of your certificate.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="3d15f-223">Você pode obter Olá válido de data e Olá toodate válida do certificado Olá baixado clicando duas vezes nele.</span><span class="sxs-lookup"><span data-stu-id="3d15f-223">You can get hello valid from date and hello valid toodate from hello downloaded certificate by double-clicking it.</span></span>  <span data-ttu-id="3d15f-224">Olá datas são listadas sob Olá **detalhes** guia.</span><span class="sxs-lookup"><span data-stu-id="3d15f-224">hello dates are listed under hello **Details** tab.</span></span>
    > 
    >
   
    <span data-ttu-id="3d15f-225">d.</span><span class="sxs-lookup"><span data-stu-id="3d15f-225">d.</span></span>  <span data-ttu-id="3d15f-226">Abra seu certificado codificado em base 64 no bloco de notas e, em seguida, Olá de copiar conteúdo dele.</span><span class="sxs-lookup"><span data-stu-id="3d15f-226">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   
    <span data-ttu-id="3d15f-227">e.</span><span class="sxs-lookup"><span data-stu-id="3d15f-227">e.</span></span>  <span data-ttu-id="3d15f-228">Em Olá **certificado** caixa de texto, conteúdo de saudação colar da área de transferência.</span><span class="sxs-lookup"><span data-stu-id="3d15f-228">In hello **Certificate** textbox, paste hello content of your clipboard.</span></span>
   
    <span data-ttu-id="3d15f-229">f.</span><span class="sxs-lookup"><span data-stu-id="3d15f-229">f.</span></span>  <span data-ttu-id="3d15f-230">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-230">Click **OK**.</span></span>

15. <span data-ttu-id="3d15f-231">Execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d15f-231">Perform hello following steps:</span></span> 
   
    <span data-ttu-id="3d15f-232">![Configuração de SSO](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "Configuração de SSO")</span><span class="sxs-lookup"><span data-stu-id="3d15f-232">![SSO configuration](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguratio.png "SSO configuration")</span></span>
   
    <span data-ttu-id="3d15f-233">a.</span><span class="sxs-lookup"><span data-stu-id="3d15f-233">a.</span></span>  <span data-ttu-id="3d15f-234">Habilitar Olá **x509 par de chaves particular**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-234">Enable hello **x509 Private Key Pair**.</span></span>
   
    <span data-ttu-id="3d15f-235">b.</span><span class="sxs-lookup"><span data-stu-id="3d15f-235">b.</span></span>  <span data-ttu-id="3d15f-236">Em Olá **ID do provedor de serviço** caixa de texto, tipo **http://www.workday.com**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-236">In hello **Service Provider ID** textbox, type **http://www.workday.com**.</span></span>
   
    <span data-ttu-id="3d15f-237">c.</span><span class="sxs-lookup"><span data-stu-id="3d15f-237">c.</span></span>  <span data-ttu-id="3d15f-238">Selecione **Habilitar a Autenticação do SAML Iniciada por SP**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-238">Select **Enable SP Initiated SAML Authentication**.</span></span>
   
    <span data-ttu-id="3d15f-239">d.</span><span class="sxs-lookup"><span data-stu-id="3d15f-239">d.</span></span>  <span data-ttu-id="3d15f-240">Em Olá portal do Azure, Olá **configurar o logon** janela, Olá cópia **Single Sign-On URL do serviço SAML** valor e, em seguida, cole-o em Olá **URL do serviço IdP SSO** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3d15f-240">In hello Azure portal, on hello **Configure sign-on** window, copy hello **SAML Single Sign-On Service URL** value, and then paste it into hello **IdP SSO Service URL** textbox.</span></span>
   
    <span data-ttu-id="3d15f-241">e.</span><span class="sxs-lookup"><span data-stu-id="3d15f-241">e.</span></span> <span data-ttu-id="3d15f-242">Selecione **Não Esvazie a Solicitação de Autenticação iniciada por SP**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-242">Select **Do Not Deflate SP-initiated Authentication Request**.</span></span>
   
    <span data-ttu-id="3d15f-243">f.</span><span class="sxs-lookup"><span data-stu-id="3d15f-243">f.</span></span> <span data-ttu-id="3d15f-244">Para **Solicitação de Método de Autenticação de Assinatura** , selecione **SHA256**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-244">As **Authentication Request Signature Method**, select **SHA256**.</span></span> 
   
    <span data-ttu-id="3d15f-245">![Método de assinatura da solicitação de autenticação](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Método de assinatura da solicitação de autenticação")</span><span class="sxs-lookup"><span data-stu-id="3d15f-245">![Authentication Request Signature Method](./media/active-directory-saas-workday-tutorial/WorkdaySSOConfiguration.png "Authentication Request Signature Method")</span></span> 
   
    <span data-ttu-id="3d15f-246">g.</span><span class="sxs-lookup"><span data-stu-id="3d15f-246">g.</span></span> <span data-ttu-id="3d15f-247">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-247">Click **OK**.</span></span> 
   
    <span data-ttu-id="3d15f-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span><span class="sxs-lookup"><span data-stu-id="3d15f-248">![OK](./media/active-directory-saas-workday-tutorial/IC782933.png "OK")
<CE></span></span>

> [!TIP]
> <span data-ttu-id="3d15f-249">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="3d15f-249">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="3d15f-250">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="3d15f-250">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="3d15f-251">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="3d15f-251">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3d15f-252">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3d15f-252">Creating an Azure AD test user</span></span>
<span data-ttu-id="3d15f-253">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d15f-253">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="3d15f-255">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3d15f-255">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d15f-256">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="3d15f-256">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3d15f-258">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-258">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3d15f-260">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d15f-260">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3d15f-262">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3d15f-262">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-workday-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3d15f-264">a.</span><span class="sxs-lookup"><span data-stu-id="3d15f-264">a.</span></span> <span data-ttu-id="3d15f-265">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-265">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d15f-266">b.</span><span class="sxs-lookup"><span data-stu-id="3d15f-266">b.</span></span> <span data-ttu-id="3d15f-267">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3d15f-267">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3d15f-268">c.</span><span class="sxs-lookup"><span data-stu-id="3d15f-268">c.</span></span> <span data-ttu-id="3d15f-269">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-269">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="3d15f-270">d.</span><span class="sxs-lookup"><span data-stu-id="3d15f-270">d.</span></span> <span data-ttu-id="3d15f-271">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-271">Click **Create**.</span></span>
 
### <a name="creating-a-workday-test-user"></a><span data-ttu-id="3d15f-272">Criação de um usuário de teste do Workday</span><span class="sxs-lookup"><span data-stu-id="3d15f-272">Creating a Workday test user</span></span>

<span data-ttu-id="3d15f-273">tooget um usuário de teste provisionado no Workday, você precisa Olá toocontact [equipe de suporte do Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html).</span><span class="sxs-lookup"><span data-stu-id="3d15f-273">tooget a test user provisioned into Workday, you need toocontact hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html).</span></span>
<span data-ttu-id="3d15f-274">Olá [equipe de suporte do Workday cliente](https://www.workday.com/en-us/partners-services/services/support.html) cria usuário Olá para você.</span><span class="sxs-lookup"><span data-stu-id="3d15f-274">hello [Workday Client support team](https://www.workday.com/en-us/partners-services/services/support.html) creates hello user for you.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="3d15f-275">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="3d15f-275">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="3d15f-276">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooWorkday.</span><span class="sxs-lookup"><span data-stu-id="3d15f-276">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkday.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="3d15f-278">**tooassign Britta Simon tooWorkday, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="3d15f-278">**tooassign Britta Simon tooWorkday, perform hello following steps:**</span></span>

1. <span data-ttu-id="3d15f-279">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-279">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="3d15f-281">Na lista de aplicativos hello, selecione **Workday**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-281">In hello applications list, select **Workday**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-workday-tutorial/tutorial_workday_app.png) 

3. <span data-ttu-id="3d15f-283">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-283">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="3d15f-285">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3d15f-285">Click **Add** button.</span></span> <span data-ttu-id="3d15f-286">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3d15f-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="3d15f-288">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="3d15f-288">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="3d15f-289">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3d15f-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3d15f-290">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="3d15f-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3d15f-291">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="3d15f-291">Testing single sign-on</span></span>

<span data-ttu-id="3d15f-292">Se você quiser tootest suas configurações de logon único, abra Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="3d15f-292">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="3d15f-293">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3d15f-293">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d15f-294">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="3d15f-294">Additional resources</span></span>

* [<span data-ttu-id="3d15f-295">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="3d15f-295">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d15f-296">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d15f-296">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="3d15f-297">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="3d15f-297">Configure User Provisioning</span></span>](active-directory-saas-workday-inbound-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-workday-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workday-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workday-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workday-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workday-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workday-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workday-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workday-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workday-tutorial/tutorial_general_203.png

