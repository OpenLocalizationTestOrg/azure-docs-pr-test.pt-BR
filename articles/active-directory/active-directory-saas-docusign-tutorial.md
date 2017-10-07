---
title: "Tutorial: integração do Azure Active Directory com o DocuSign | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e o DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a691288b-84c1-40fb-84bd-5b06878865f0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: e4ef40b8f5af20d811d8d806d2bd7e2039c55052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-docusign"></a><span data-ttu-id="a6ce0-103">Tutorial: integração do Active Directory do Azure com o DocuSign</span><span class="sxs-lookup"><span data-stu-id="a6ce0-103">Tutorial: Azure Active Directory integration with DocuSign</span></span>

<span data-ttu-id="a6ce0-104">Neste tutorial, você aprenderá como toointegrate DocuSign com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="a6ce0-104">In this tutorial, you learn how toointegrate DocuSign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a6ce0-105">Integrando o DocuSign com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6ce0-105">Integrating DocuSign with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a6ce0-106">Você pode controlar no AD do Azure que tenha acesso tooDocuSign</span><span class="sxs-lookup"><span data-stu-id="a6ce0-106">You can control in Azure AD who has access tooDocuSign</span></span>
- <span data-ttu-id="a6ce0-107">Você pode habilitar seu usuários tooautomatically get conectado tooDocuSign (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a6ce0-107">You can enable your users tooautomatically get signed-on tooDocuSign (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a6ce0-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="a6ce0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a6ce0-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a6ce0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a6ce0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a6ce0-110">Prerequisites</span></span>

<span data-ttu-id="a6ce0-111">tooconfigure integração do AD do Azure com o DocuSign, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6ce0-111">tooconfigure Azure AD integration with DocuSign, you need hello following items:</span></span>

- <span data-ttu-id="a6ce0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a6ce0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a6ce0-113">Uma assinatura habilitada para logon único do DocuSign</span><span class="sxs-lookup"><span data-stu-id="a6ce0-113">A DocuSign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a6ce0-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a6ce0-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="a6ce0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a6ce0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a6ce0-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a6ce0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a6ce0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="a6ce0-118">Scenario description</span></span>
<span data-ttu-id="a6ce0-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a6ce0-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="a6ce0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a6ce0-121">Adicionando DocuSign da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a6ce0-121">Adding DocuSign from hello gallery</span></span>
2. <span data-ttu-id="a6ce0-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a6ce0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-docusign-from-hello-gallery"></a><span data-ttu-id="a6ce0-123">Adicionando DocuSign da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="a6ce0-123">Adding DocuSign from hello gallery</span></span>
<span data-ttu-id="a6ce0-124">integração de saudação tooconfigure do DocuSign no AD do Azure, você precisa tooadd DocuSign na lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-124">tooconfigure hello integration of DocuSign into Azure AD, you need tooadd DocuSign from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a6ce0-125">**tooadd DocuSign da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a6ce0-125">**tooadd DocuSign from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6ce0-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a6ce0-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a6ce0-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="a6ce0-131">Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="a6ce0-133">Na caixa de pesquisa hello, digite **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-133">In hello search box, type **DocuSign**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_search.png)

5. <span data-ttu-id="a6ce0-135">No painel de resultados de saudação, selecione **DocuSign**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-135">In hello results panel, select **DocuSign**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a6ce0-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a6ce0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a6ce0-138">Nesta seção, você configura e testa o logon único do Azure AD com o DocuSign, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-138">In this section, you configure and test Azure AD single sign-on with DocuSign based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a6ce0-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no DocuSign é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in DocuSign is tooa user in Azure AD.</span></span> <span data-ttu-id="a6ce0-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no DocuSign precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-140">In other words, a link relationship between an Azure AD user and hello related user in DocuSign needs toobe established.</span></span>

<span data-ttu-id="a6ce0-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** no DocuSign.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in DocuSign.</span></span>

<span data-ttu-id="a6ce0-142">tooconfigure e teste de logon único do AD do Azure com o DocuSign, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6ce0-142">tooconfigure and test Azure AD single sign-on with DocuSign, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a6ce0-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a6ce0-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a6ce0-145">**[Criar um usuário de teste do DocuSign](#creating-a-docusign-test-user)**  -toohave um equivalente do Britta Simon no DocuSign que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-145">**[Creating a DocuSign test user](#creating-a-docusign-test-user)** - toohave a counterpart of Britta Simon in DocuSign that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a6ce0-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a6ce0-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a6ce0-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="a6ce0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a6ce0-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do DocuSign.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your DocuSign application.</span></span>

<span data-ttu-id="a6ce0-150">**tooconfigure AD do Azure-logon único com o DocuSign, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a6ce0-150">**tooconfigure Azure AD single sign-on with DocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6ce0-151">Em Olá portal do Azure, Olá **DocuSign** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-151">In hello Azure portal, on hello **DocuSign** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="a6ce0-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_samlbase.png)

3. <span data-ttu-id="a6ce0-155">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base 64)** e, em seguida, salve o arquivo do certificado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-155">On hello **SAML Signing Certificate** section, click **Certificate(Base 64)** and then save certificate file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_certificate.png) 

4. <span data-ttu-id="a6ce0-157">Em Olá **DocuSign configuração** seção do portal do Azure, clique em **DocuSign configurar** tooopen configurar o logon na janela.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-157">On hello **DocuSign Configuration** section of Azure portal, Click **Configure DocuSign** tooopen Configure sign-on window.</span></span> <span data-ttu-id="a6ce0-158">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="a6ce0-158">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_configure.png)

5. <span data-ttu-id="a6ce0-160">Em uma janela de navegador web diferente, o logon tooyour **portal de administração do DocuSign** como um administrador.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-160">In a different web browser window, login tooyour **DocuSign admin portal** as an administrator.</span></span>

6. <span data-ttu-id="a6ce0-161">No menu de navegação Olá Olá esquerda, clique em **domínios**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-161">In hello navigation menu on hello left, click **Domains**.</span></span>
   
    ![Configurando o logon único][51]

7. <span data-ttu-id="a6ce0-163">No painel direito da saudação, clique em **declaração domínio**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-163">On hello right pane, click **Claim Domain**.</span></span>
   
    ![Configurando o logon único][52]

8. <span data-ttu-id="a6ce0-165">Em Olá **de declaração de um domínio** caixa de diálogo, na Olá **nome de domínio** caixa de texto, digite o domínio da sua empresa e, em seguida, clique em **declaração**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-165">On hello **Claim a domain** dialog, in hello **Domain Name** textbox, type your company domain, and then click **Claim**.</span></span> <span data-ttu-id="a6ce0-166">Certificar-se de que você verificar domínio hello e Olá status está ativo.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-166">Make sure that you verify hello domain and hello status is active.</span></span>
   
    ![Configurando o logon único][53]

9. <span data-ttu-id="a6ce0-168">No menu no lado esquerdo do hello, clique em **provedores de identidade**</span><span class="sxs-lookup"><span data-stu-id="a6ce0-168">In menu on hello left side, click **Identity Providers**</span></span>  
   
    ![Configurando o logon único][54]
10. <span data-ttu-id="a6ce0-170">No painel direito da saudação, clique em **Adicionar provedor de identidade**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-170">In hello right pane, click **Add Identity Provider**.</span></span> 
   
    ![Configurando o logon único][55]

11. <span data-ttu-id="a6ce0-172">Em Olá **as configurações do provedor de identidade** página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6ce0-172">On hello **Identity Provider Settings** page, perform hello following steps:</span></span>
   
    ![Configurando o logon único][56]

    <span data-ttu-id="a6ce0-174">a.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-174">a.</span></span> <span data-ttu-id="a6ce0-175">Em Olá **nome** caixa de texto, digite um nome exclusivo para a sua configuração.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-175">In hello **Name** textbox, type a unique name for your configuration.</span></span> <span data-ttu-id="a6ce0-176">Não use espaços.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-176">Do not use spaces.</span></span>

    <span data-ttu-id="a6ce0-177">b.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-177">b.</span></span> <span data-ttu-id="a6ce0-178">Colar **ID da entidade SAML** em Olá **emissor do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-178">Paste **SAML Entity ID** into hello **Identity Provider Issuer** textbox.</span></span>

    <span data-ttu-id="a6ce0-179">c.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-179">c.</span></span> <span data-ttu-id="a6ce0-180">Colar **Single Sign-On URL do serviço SAML** em Olá **URL de logon do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-180">Paste **SAML Single Sign-On Service URL** into hello **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="a6ce0-181">d.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-181">d.</span></span> <span data-ttu-id="a6ce0-182">Colar **URL de logout** em Olá **URL de Logout do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-182">Paste **Sign-Out URL** into hello **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="a6ce0-183">e.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-183">e.</span></span> <span data-ttu-id="a6ce0-184">Selecione **Assinar Solicitação AuthN**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-184">Select **Sign AuthN Request**.</span></span>

    <span data-ttu-id="a6ce0-185">f.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-185">f.</span></span> <span data-ttu-id="a6ce0-186">Para **Enviar solicitação AuthN por**, selecione **POST**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-186">As **Send AuthN request by**, select **POST**.</span></span>

    <span data-ttu-id="a6ce0-187">g.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-187">g.</span></span> <span data-ttu-id="a6ce0-188">Em **Enviar solicitação de logoff por**, selecione **GET**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-188">As **Send logout request by**, select **GET**.</span></span>

12. <span data-ttu-id="a6ce0-189">Em Olá **mapeamento de atributo personalizado** , escolha o campo Olá deseja toomap com declaração do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-189">In hello **Custom Attribute Mapping** section, choose hello field you want toomap with Azure AD Claim.</span></span> <span data-ttu-id="a6ce0-190">Neste exemplo, Olá **emailaddress** declaração é mapeada com valor de saudação do **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-190">In this example, hello **emailaddress** claim is mapped with hello value of **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span> <span data-ttu-id="a6ce0-191">É o nome da declaração saudação padrão do AD do Azure para declaração de email.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-191">It is hello default claim name from Azure AD for email claim.</span></span> 
   
    > [!NOTE]
    > <span data-ttu-id="a6ce0-192">Saudação de uso apropriada **identificador de usuário** toomap usuário de saudação do mapeamento de usuário do AD do Azure tooDocuSign.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-192">Use hello appropriate **User identifier** toomap hello user from Azure AD tooDocuSign user mapping.</span></span> <span data-ttu-id="a6ce0-193">Selecione Olá campo apropriado e insira o valor apropriado de saudação com base nas configurações de sua organização.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-193">Select hello proper Field and enter hello appropriate value based on your organization settings.</span></span>
          
    ![Configurando o logon único][57]

13. <span data-ttu-id="a6ce0-195">Em Olá **certificado do provedor de identidade** seção, clique em **Adicionar certificado**e, em seguida, carregue o certificado de saudação que baixou do portal do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-195">In hello **Identity Provider Certificate** section, click **Add Certificate**, and then upload hello certificate you have downloaded from Azure AD portal.</span></span>   
   
    ![Configurando o logon único][58]

14. <span data-ttu-id="a6ce0-197">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-197">Click **Save**.</span></span>

15. <span data-ttu-id="a6ce0-198">Em Olá **provedores de identidade** seção, clique em **ações**e, em seguida, clique em **pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-198">In hello **Identity Providers** section, click **Actions**, and then click **Endpoints**.</span></span>   
   
    ![Configurando o logon único][59]
 
16. <span data-ttu-id="a6ce0-200">Em Olá **exibir pontos de extremidade do SAML 2.0** seção **portal de administração do DocuSign**, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6ce0-200">In hello **View SAML 2.0 Endpoints** section on **DocuSign admin portal**, perform hello following steps:</span></span>
   
    ![Configurando o logon único][60]
   
    <span data-ttu-id="a6ce0-202">a.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-202">a.</span></span> <span data-ttu-id="a6ce0-203">Saudação de cópia **URL do emissor de provedor de serviço**e, em seguida, cole a saudação **identificador** textbox em **DocuSign domínio e URLs** seção Olá Olá seguinte de portal do Azure padrão: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-203">Copy hello **Service Provider Issuer URL**, and then paste into hello **Identifier** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/login/sp/<uniqueID>`.</span></span>
   
    <span data-ttu-id="a6ce0-204">b.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-204">b.</span></span> <span data-ttu-id="a6ce0-205">Saudação de cópia **URL de logon do provedor de serviço**e, em seguida, cole a saudação **URL de logon** textbox em **DocuSign domínio e URLs** seção Olá Olá seguinte de portal do Azure padrão: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-205">Copy hello **Service Provider Login URL**, and then paste into hello **Sign On URL** textbox on **DocuSign Domain and URLs** section of hello Azure portal following hello pattern: `https://<subdomain>.docusign.com/organization/<uniqueID>/saml2/`.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_url.png)
      
    <span data-ttu-id="a6ce0-207">c.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-207">c.</span></span>  <span data-ttu-id="a6ce0-208">Clique em **Fechar**</span><span class="sxs-lookup"><span data-stu-id="a6ce0-208">Click **Close**</span></span>
    
17. <span data-ttu-id="a6ce0-209">No portal do Azure de Olá, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-209">On hello Azure portal, click **Save**.</span></span>
    
    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="a6ce0-211">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="a6ce0-211">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a6ce0-212">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-212">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a6ce0-213">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a6ce0-213">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a6ce0-214">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a6ce0-214">Creating an Azure AD test user</span></span>
<span data-ttu-id="a6ce0-215">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-215">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="a6ce0-217">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a6ce0-217">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6ce0-218">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-218">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a6ce0-220">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-220">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a6ce0-222">Na parte superior de saudação da caixa de diálogo hello, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-222">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a6ce0-224">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a6ce0-224">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-docusign-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a6ce0-226">a.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-226">a.</span></span> <span data-ttu-id="a6ce0-227">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-227">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a6ce0-228">b.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-228">b.</span></span> <span data-ttu-id="a6ce0-229">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-229">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a6ce0-230">c.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-230">c.</span></span> <span data-ttu-id="a6ce0-231">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-231">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a6ce0-232">d.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-232">d.</span></span> <span data-ttu-id="a6ce0-233">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-233">Click **Create**.</span></span>
 
### <a name="creating-a-docusign-test-user"></a><span data-ttu-id="a6ce0-234">Criando um usuário de teste do DocuSign</span><span class="sxs-lookup"><span data-stu-id="a6ce0-234">Creating a DocuSign test user</span></span>

<span data-ttu-id="a6ce0-235">Aplicativo dá suporte a **apenas durante o provisionamento do usuário** e depois que os usuários de autenticação são criados automaticamente no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-235">Application supports **Just in time user provisioning** and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a6ce0-236">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="a6ce0-236">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a6ce0-237">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo tooDocuSign seu acesso.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-237">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooDocuSign.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="a6ce0-239">**tooassign Britta Simon tooDocuSign, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="a6ce0-239">**tooassign Britta Simon tooDocuSign, perform hello following steps:**</span></span>

1. <span data-ttu-id="a6ce0-240">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-240">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="a6ce0-242">Na lista de aplicativos hello, selecione **DocuSign**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-242">In hello applications list, select **DocuSign**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-docusign-tutorial/tutorial_docusign_app.png) 

3. <span data-ttu-id="a6ce0-244">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-244">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="a6ce0-246">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-246">Click **Add** button.</span></span> <span data-ttu-id="a6ce0-247">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-247">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="a6ce0-249">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-249">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a6ce0-250">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-250">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a6ce0-251">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-251">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a6ce0-252">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="a6ce0-252">Testing single sign-on</span></span>

<span data-ttu-id="a6ce0-253">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-253">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a6ce0-254">Quando você clica em bloco DocuSign Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour DocuSign aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a6ce0-254">When you click hello DocuSign tile in hello Access Panel, you should get automatically signed-on tooyour DocuSign application.</span></span>
<span data-ttu-id="a6ce0-255">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a6ce0-255">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a6ce0-256">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="a6ce0-256">Additional resources</span></span>

* [<span data-ttu-id="a6ce0-257">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="a6ce0-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a6ce0-258">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a6ce0-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="a6ce0-259">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="a6ce0-259">Configure User Provisioning</span></span>](active-directory-saas-docusign-provisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_04.png
[51]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_21.png
[52]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_22.png
[53]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_23.png
[54]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_19.png
[55]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_20.png
[56]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_24.png
[57]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_25.png
[58]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_26.png
[59]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_27.png
[60]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_28.png
[61]: ./media/active-directory-saas-docusign-tutorial/tutorial_docusign_29.png
[100]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-docusign-tutorial/tutorial_general_203.png

