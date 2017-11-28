---
title: "Tutorial: Integração do Azure Active Directory ao ScreenSteps | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e ScreenSteps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 4563fe94-a88f-4895-a07f-79df44889cf9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jeedes
ms.openlocfilehash: fd041e5fe4552727eeda2dabc1773d8043d410f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-screensteps"></a><span data-ttu-id="d38eb-103">Tutorial: Integração do Active Directory do Azure com o ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="d38eb-103">Tutorial: Azure Active Directory integration with ScreenSteps</span></span>

<span data-ttu-id="d38eb-104">Neste tutorial, você aprenderá como toointegrate ScreenSteps com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="d38eb-104">In this tutorial, you learn how toointegrate ScreenSteps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d38eb-105">Integrando o ScreenSteps com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="d38eb-105">Integrating ScreenSteps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d38eb-106">Você pode controlar no AD do Azure que tenha acesso tooScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="d38eb-106">You can control in Azure AD who has access tooScreenSteps.</span></span>
- <span data-ttu-id="d38eb-107">Você pode habilitar seus usuários tooautomatically get conectado tooScreenSteps (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d38eb-107">You can enable your users tooautomatically get signed-on tooScreenSteps (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d38eb-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d38eb-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="d38eb-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d38eb-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d38eb-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d38eb-110">Prerequisites</span></span>

<span data-ttu-id="d38eb-111">tooconfigure integração do AD do Azure com o ScreenSteps, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="d38eb-111">tooconfigure Azure AD integration with ScreenSteps, you need hello following items:</span></span>

- <span data-ttu-id="d38eb-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d38eb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d38eb-113">Uma assinatura do ScreenSteps habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="d38eb-113">A ScreenSteps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d38eb-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="d38eb-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d38eb-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="d38eb-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d38eb-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="d38eb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d38eb-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d38eb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d38eb-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="d38eb-118">Scenario description</span></span>
<span data-ttu-id="d38eb-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="d38eb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d38eb-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="d38eb-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d38eb-121">Adicionando ScreenSteps da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d38eb-121">Adding ScreenSteps from hello gallery</span></span>
2. <span data-ttu-id="d38eb-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d38eb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-screensteps-from-hello-gallery"></a><span data-ttu-id="d38eb-123">Adicionando ScreenSteps da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="d38eb-123">Adding ScreenSteps from hello gallery</span></span>
<span data-ttu-id="d38eb-124">integração de saudação tooconfigure do ScreenSteps no AD do Azure, você precisa tooadd ScreenSteps da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="d38eb-124">tooconfigure hello integration of ScreenSteps into Azure AD, you need tooadd ScreenSteps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d38eb-125">**tooadd ScreenSteps da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d38eb-125">**tooadd ScreenSteps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d38eb-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="d38eb-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="d38eb-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d38eb-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="d38eb-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d38eb-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="d38eb-133">Na caixa de pesquisa hello, digite **ScreenSteps**, selecione **ScreenSteps** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="d38eb-133">In hello search box, type **ScreenSteps**, select **ScreenSteps** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ScreenSteps na lista de resultados de saudação](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d38eb-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d38eb-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d38eb-136">Nesta seção, você configurará e testará o logon único do Azure AD com o ScreenSteps, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="d38eb-136">In this section, you configure and test Azure AD single sign-on with ScreenSteps based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d38eb-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no ScreenSteps é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="d38eb-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ScreenSteps is tooa user in Azure AD.</span></span> <span data-ttu-id="d38eb-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em ScreenSteps precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="d38eb-138">In other words, a link relationship between an Azure AD user and hello related user in ScreenSteps needs toobe established.</span></span>

<span data-ttu-id="d38eb-139">ScreenSteps, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38eb-139">In ScreenSteps, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d38eb-140">tooconfigure e teste de logon único do AD do Azure com o ScreenSteps, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="d38eb-140">tooconfigure and test Azure AD single sign-on with ScreenSteps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d38eb-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="d38eb-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d38eb-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d38eb-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d38eb-143">**[Criar um usuário de teste do ScreenSteps](#create-a-screensteps-test-user)**  -toohave um equivalente do Britta Simon em ScreenSteps é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="d38eb-143">**[Create a ScreenSteps test user](#create-a-screensteps-test-user)** - toohave a counterpart of Britta Simon in ScreenSteps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d38eb-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="d38eb-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d38eb-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="d38eb-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d38eb-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d38eb-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d38eb-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="d38eb-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ScreenSteps application.</span></span>

<span data-ttu-id="d38eb-148">**tooconfigure AD do Azure-logon único com o ScreenSteps, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d38eb-148">**tooconfigure Azure AD single sign-on with ScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="d38eb-149">Em Olá portal do Azure, Olá **ScreenSteps** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-149">In hello Azure portal, on hello **ScreenSteps** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="d38eb-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="d38eb-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_samlbase.png)

3. <span data-ttu-id="d38eb-153">Em Olá **ScreenSteps domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d38eb-153">On hello **ScreenSteps Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_url.png)

    <span data-ttu-id="d38eb-155">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenantname>.ScreenSteps.com`</span><span class="sxs-lookup"><span data-stu-id="d38eb-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenantname>.ScreenSteps.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d38eb-156">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="d38eb-156">This value is not real.</span></span> <span data-ttu-id="d38eb-157">Atualize esse valor com hello real URL de entrada, que é explicada mais adiante neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="d38eb-157">Update this value with hello actual Sign-On URL, which is explained later in this tutorial.</span></span> 

4. <span data-ttu-id="d38eb-158">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="d38eb-158">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_certificate.png) 

5. <span data-ttu-id="d38eb-160">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="d38eb-160">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-screensteps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d38eb-162">Em Olá **ScreenSteps configuração** seção, clique em **configurar ScreenSteps** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="d38eb-162">On hello **ScreenSteps Configuration** section, click **Configure ScreenSteps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d38eb-163">Saudação de cópia **URL de logout e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="d38eb-163">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do ScreenSteps](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_configure.png) 

7. <span data-ttu-id="d38eb-165">Em outra janela do navegador da Web, faça logon em seu site de empresa ScreenSteps como um administrador.</span><span class="sxs-lookup"><span data-stu-id="d38eb-165">In a different web browser window, log into your ScreenSteps company site as an administrator.</span></span>

8. <span data-ttu-id="d38eb-166">Clique em **Configurações da Conta**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-166">Click **Account Settings**.</span></span>

    <span data-ttu-id="d38eb-167">![Gerenciamento de contas](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Gerenciamento de contas")</span><span class="sxs-lookup"><span data-stu-id="d38eb-167">![Account management](./media/active-directory-saas-screensteps-tutorial/ic778523.png "Account management")</span></span>

9. <span data-ttu-id="d38eb-168">Clique em **Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-168">Click **Single Sign-on**.</span></span>

    <span data-ttu-id="d38eb-169">![Autenticação Remota](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Autenticação Remota")</span><span class="sxs-lookup"><span data-stu-id="d38eb-169">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778524.png "Remote authentication")</span></span>

10. <span data-ttu-id="d38eb-170">Clique em  **Criar Ponto de Extremidade de Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-170">Click **Create Single Sign-on Endpoint**.</span></span>

    <span data-ttu-id="d38eb-171">![Autenticação Remota](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Autenticação Remota")</span><span class="sxs-lookup"><span data-stu-id="d38eb-171">![Remote authentication](./media/active-directory-saas-screensteps-tutorial/ic778525.png "Remote authentication")</span></span>

11. <span data-ttu-id="d38eb-172">Em Olá **criar único logon no ponto de extremidade** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d38eb-172">In hello **Create Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="d38eb-173">![Criar um Ponto de Extremidade de Autenticação](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Criar um Ponto de Extremidade de Autenticação")</span><span class="sxs-lookup"><span data-stu-id="d38eb-173">![Create an authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778526.png "Create an authentication endpoint")</span></span>
    
    <span data-ttu-id="d38eb-174">a.</span><span class="sxs-lookup"><span data-stu-id="d38eb-174">a.</span></span> <span data-ttu-id="d38eb-175">Em Olá **título** caixa de texto, digite um título.</span><span class="sxs-lookup"><span data-stu-id="d38eb-175">In hello **Title** textbox, type a title.</span></span>
    
    <span data-ttu-id="d38eb-176">b.</span><span class="sxs-lookup"><span data-stu-id="d38eb-176">b.</span></span> <span data-ttu-id="d38eb-177">De saudação **modo** lista, selecione **SAML**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-177">From hello **Mode** list, select **SAML**.</span></span>
    
    <span data-ttu-id="d38eb-178">c.</span><span class="sxs-lookup"><span data-stu-id="d38eb-178">c.</span></span> <span data-ttu-id="d38eb-179">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-179">Click **Create**.</span></span>

12. <span data-ttu-id="d38eb-180">**Editar** Olá novo ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="d38eb-180">**Edit** hello new endpoint.</span></span>

    <span data-ttu-id="d38eb-181">![Editar ponto de extremidade](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Editar ponto de extremidade")</span><span class="sxs-lookup"><span data-stu-id="d38eb-181">![Edit endpoint](./media/active-directory-saas-screensteps-tutorial/ic778528.png "Edit endpoint")</span></span>

13. <span data-ttu-id="d38eb-182">Em Olá **Editar único logon no ponto de extremidade** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d38eb-182">In hello **Edit Single Sign-on Endpoint** section, perform hello following steps:</span></span>

    <span data-ttu-id="d38eb-183">![Ponto de Extremidade de Autenticação Remota](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Ponto de Extremidade de Autenticação Remota")</span><span class="sxs-lookup"><span data-stu-id="d38eb-183">![Remote authentication endpoint](./media/active-directory-saas-screensteps-tutorial/ic778527.png "Remote authentication endpoint")</span></span>

    <span data-ttu-id="d38eb-184">a.</span><span class="sxs-lookup"><span data-stu-id="d38eb-184">a.</span></span> <span data-ttu-id="d38eb-185">Clique em **novo arquivo de certificado SAML carregamento**e, em seguida, carregar Olá certificado, que você baixou do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d38eb-185">Click **Upload new SAML Certificate file**, and then upload hello certificate, which you have downloaded from Azure portal.</span></span>
    
    <span data-ttu-id="d38eb-186">b.</span><span class="sxs-lookup"><span data-stu-id="d38eb-186">b.</span></span> <span data-ttu-id="d38eb-187">Colar **Single Sign-On URL do serviço SAML** valor que você copiou de saudação portal do Azure em hello **URL de logon remoto** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="d38eb-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **Remote Login URL** textbox.</span></span>
    
    <span data-ttu-id="d38eb-188">c.</span><span class="sxs-lookup"><span data-stu-id="d38eb-188">c.</span></span> <span data-ttu-id="d38eb-189">Colar **URL de logout** valor que você copiou de saudação portal do Azure em hello **URL de logoff** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="d38eb-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **Log out URL** textbox.</span></span>
    
    <span data-ttu-id="d38eb-190">d.</span><span class="sxs-lookup"><span data-stu-id="d38eb-190">d.</span></span> <span data-ttu-id="d38eb-191">Selecione um **grupo** tooassign toowhen de usuários que são provisionados.</span><span class="sxs-lookup"><span data-stu-id="d38eb-191">Select a **Group** tooassign users toowhen they are provisioned.</span></span>
    
    <span data-ttu-id="d38eb-192">e.</span><span class="sxs-lookup"><span data-stu-id="d38eb-192">e.</span></span> <span data-ttu-id="d38eb-193">Clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-193">Click **Update**.</span></span>

    <span data-ttu-id="d38eb-194">f.</span><span class="sxs-lookup"><span data-stu-id="d38eb-194">f.</span></span> <span data-ttu-id="d38eb-195">Saudação de cópia **SAML consumidor URL** toohello área de transferência e cole no toohello **URL de logon** textbox em **ScreenSteps domínio e URLs** seção.</span><span class="sxs-lookup"><span data-stu-id="d38eb-195">Copy hello **SAML Consumer URL** toohello clipboard and paste in toohello **Sign-on URL** textbox in **ScreenSteps Domain and URLs** section.</span></span>
    
    <span data-ttu-id="d38eb-196">g.</span><span class="sxs-lookup"><span data-stu-id="d38eb-196">g.</span></span> <span data-ttu-id="d38eb-197">Retornar toohello **Editar único logon no ponto de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-197">Return toohello **Edit Single Sign-on Endpoint**.</span></span>
    
    <span data-ttu-id="d38eb-198">h.</span><span class="sxs-lookup"><span data-stu-id="d38eb-198">h.</span></span> <span data-ttu-id="d38eb-199">Clique em Olá **tornar padrão para a conta** botão toouse esse ponto de extremidade para todos os usuários que fizerem logon em ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="d38eb-199">Click hello **Make default for account** button toouse this endpoint for all users who log into ScreenSteps.</span></span> <span data-ttu-id="d38eb-200">Como alternativa, você pode clicar Olá **adicionar tooSite** botão toouse esse ponto de extremidade para sites específicos em **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-200">Alternatively you can click hello **Add tooSite** button toouse this endpoint for specific sites in **ScreenSteps**.</span></span>

> [!TIP]
> <span data-ttu-id="d38eb-201">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="d38eb-201">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d38eb-202">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="d38eb-202">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d38eb-203">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d38eb-203">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d38eb-204">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="d38eb-204">Create an Azure AD test user</span></span>

<span data-ttu-id="d38eb-205">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d38eb-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="d38eb-207">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d38eb-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d38eb-208">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="d38eb-208">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-screensteps-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d38eb-210">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-210">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-screensteps-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d38eb-212">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d38eb-212">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-screensteps-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d38eb-214">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d38eb-214">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-screensteps-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d38eb-216">a.</span><span class="sxs-lookup"><span data-stu-id="d38eb-216">a.</span></span> <span data-ttu-id="d38eb-217">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-217">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d38eb-218">b.</span><span class="sxs-lookup"><span data-stu-id="d38eb-218">b.</span></span> <span data-ttu-id="d38eb-219">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d38eb-219">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="d38eb-220">c.</span><span class="sxs-lookup"><span data-stu-id="d38eb-220">c.</span></span> <span data-ttu-id="d38eb-221">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="d38eb-221">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="d38eb-222">d.</span><span class="sxs-lookup"><span data-stu-id="d38eb-222">d.</span></span> <span data-ttu-id="d38eb-223">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-223">Click **Create**.</span></span>
 
### <a name="create-a-screensteps-test-user"></a><span data-ttu-id="d38eb-224">Criar um usuário de teste do ScreenSteps</span><span class="sxs-lookup"><span data-stu-id="d38eb-224">Create a ScreenSteps test user</span></span>

<span data-ttu-id="d38eb-225">Nesta seção, você criará um usuário chamado Brenda Fernandes no ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="d38eb-225">In this section, you create a user called Britta Simon in ScreenSteps.</span></span> <span data-ttu-id="d38eb-226">Trabalhar com [equipe de suporte do cliente ScreenSteps](https://www.screensteps.com/contact) para adicionar usuários de saudação na plataforma do ScreenSteps hello.</span><span class="sxs-lookup"><span data-stu-id="d38eb-226">Work with [ScreenSteps Client support team](https://www.screensteps.com/contact) to add hello users in hello ScreenSteps platform.</span></span> <span data-ttu-id="d38eb-227">Os usuários devem ser criados e ativados antes de usar o logon único.</span><span class="sxs-lookup"><span data-stu-id="d38eb-227">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="d38eb-228">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="d38eb-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="d38eb-229">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="d38eb-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooScreenSteps.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="d38eb-231">**tooassign Britta Simon tooScreenSteps, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="d38eb-231">**tooassign Britta Simon tooScreenSteps, perform hello following steps:**</span></span>

1. <span data-ttu-id="d38eb-232">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="d38eb-234">Na lista de aplicativos hello, selecione **ScreenSteps**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-234">In hello applications list, select **ScreenSteps**.</span></span>

    ![link de ScreenSteps Olá na lista de aplicativos Olá](./media/active-directory-saas-screensteps-tutorial/tutorial_screensteps_app.png)  

3. <span data-ttu-id="d38eb-236">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="d38eb-238">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="d38eb-238">Click **Add** button.</span></span> <span data-ttu-id="d38eb-239">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d38eb-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="d38eb-241">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38eb-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d38eb-242">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d38eb-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d38eb-243">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="d38eb-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d38eb-244">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="d38eb-244">Test single sign-on</span></span>

<span data-ttu-id="d38eb-245">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="d38eb-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d38eb-246">Quando você clica em Olá ScreenSteps bloco no painel de acesso de saudação, você deve obter tooyour automaticamente conectado no aplicativo ScreenSteps.</span><span class="sxs-lookup"><span data-stu-id="d38eb-246">When you click hello ScreenSteps tile in hello Access Panel, you should get automatically signed-on tooyour ScreenSteps application.</span></span>
<span data-ttu-id="d38eb-247">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d38eb-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d38eb-248">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="d38eb-248">Additional resources</span></span>

* [<span data-ttu-id="d38eb-249">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="d38eb-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d38eb-250">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d38eb-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-screensteps-tutorial/tutorial_general_203.png

