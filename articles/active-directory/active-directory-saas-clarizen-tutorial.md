---
title: "Tutorial: Integração do Azure Active Directory ao Clarizen | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Clarizen."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: f24ccda3b90e5df9a203a444dfda905043b30276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clarizen"></a><span data-ttu-id="04d3f-103">Tutorial: integração do Active Directory do Azure ao Clarizen</span><span class="sxs-lookup"><span data-stu-id="04d3f-103">Tutorial: Azure Active Directory integration with Clarizen</span></span>

<span data-ttu-id="04d3f-104">Neste tutorial, você aprenderá como toointegrate do Azure Active Directory (AD do Azure) com o Clarizen.</span><span class="sxs-lookup"><span data-stu-id="04d3f-104">In this tutorial, you learn how toointegrate Azure Active Directory (Azure AD) with Clarizen.</span></span> <span data-ttu-id="04d3f-105">Isso proporciona integração Olá seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="04d3f-105">This integration gives you hello following benefits:</span></span>

- <span data-ttu-id="04d3f-106">Você pode controlar, no AD do Azure, que tem acesso tooClarizen.</span><span class="sxs-lookup"><span data-stu-id="04d3f-106">You can control, in Azure AD, who has access tooClarizen.</span></span>
- <span data-ttu-id="04d3f-107">Você pode habilitar o toobe de usuários conectado automaticamente tooClarizen (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="04d3f-107">You can enable your users toobe automatically signed in tooClarizen (single sign-on) with their Azure AD accounts.</span></span>
- <span data-ttu-id="04d3f-108">Você pode gerenciar suas contas em um local central, Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="04d3f-108">You can manage your accounts in one central location, hello Azure portal.</span></span>

<span data-ttu-id="04d3f-109">cenário de saudação neste tutorial consiste em duas tarefas principais:</span><span class="sxs-lookup"><span data-stu-id="04d3f-109">hello scenario in this tutorial consists of two main tasks:</span></span>

1. <span data-ttu-id="04d3f-110">Adicione Clarizen da Galeria de saudação.</span><span class="sxs-lookup"><span data-stu-id="04d3f-110">Add Clarizen from hello gallery.</span></span>
2. <span data-ttu-id="04d3f-111">Configurar e testar logon único do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="04d3f-111">Configure and test Azure AD single sign-on.</span></span>

<span data-ttu-id="04d3f-112">Para conhecer mais detalhadamente a integração de aplicativos de SaaS (software como serviço) ao Azure AD, consulte [O que é o acesso a aplicativos e logon único com o Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="04d3f-112">If you want more details about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04d3f-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="04d3f-113">Prerequisites</span></span>
<span data-ttu-id="04d3f-114">tooconfigure integração do AD do Azure com o Clarizen, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="04d3f-114">tooconfigure Azure AD integration with Clarizen, you need hello following items:</span></span>

- <span data-ttu-id="04d3f-115">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="04d3f-115">An Azure AD subscription</span></span>
- <span data-ttu-id="04d3f-116">Uma assinatura de Clarizen está habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="04d3f-116">A Clarizen subscription that's enabled for single sign-on</span></span>

<span data-ttu-id="04d3f-117">etapas de saudação tootest neste tutorial, siga estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="04d3f-117">tootest hello steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="04d3f-118">Teste o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="04d3f-118">Test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="04d3f-119">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="04d3f-119">Don't use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="04d3f-120">Se não tiver um ambiente de teste do Azure AD, você poderá [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="04d3f-120">If you don't have an Azure AD test environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="add-clarizen-from-hello-gallery"></a><span data-ttu-id="04d3f-121">Adicionar Clarizen da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="04d3f-121">Add Clarizen from hello gallery</span></span>
<span data-ttu-id="04d3f-122">integração de saudação do tooconfigure do Clarizen no AD do Azure, adicione Clarizen da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="04d3f-122">tooconfigure hello integration of Clarizen into Azure AD, add Clarizen from hello gallery tooyour list of managed SaaS apps.</span></span>

1. <span data-ttu-id="04d3f-123">Em Olá [portal do Azure](https://portal.azure.com), no painel esquerdo de hello, clique Olá **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="04d3f-123">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Ícone do Azure Active Directory][1]

2. <span data-ttu-id="04d3f-125">Clique em **Aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-125">Click **Enterprise applications**.</span></span> <span data-ttu-id="04d3f-126">Em seguida, clique em **Todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-126">Then click **All applications**.</span></span>

    ![Clicar em "Aplicativos corporativos" e em "Todos os aplicativos"][2]

3. <span data-ttu-id="04d3f-128">Clique em Olá **adicionar** botão na parte superior de Olá Olá da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="04d3f-128">Click hello **Add** button at hello top of hello dialog box.</span></span>

    ![botão de "Adicionar" Hello][3]

4. <span data-ttu-id="04d3f-130">Na caixa de pesquisa hello, digite **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-130">In hello search box, type **Clarizen**.</span></span>

    ![Digitar "Clarizen" na caixa de pesquisa de saudação](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_000.png)

5. <span data-ttu-id="04d3f-132">No painel de resultados de saudação, selecione **Clarizen**e, em seguida, clique em **adicionar** aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="04d3f-132">In hello results pane, select **Clarizen**, and then click **Add** tooadd hello application.</span></span>

    ![Selecionando Clarizen no painel de resultados de saudação](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_0001.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="04d3f-134">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="04d3f-134">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="04d3f-135">Em Olá seções a seguir, configurar e testar o logon único do AD do Azure com o Clarizen com base no usuário de teste Olá Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="04d3f-135">In hello following sections, you configure and test Azure AD single sign-on with Clarizen based on hello test user Britta Simon.</span></span>

<span data-ttu-id="04d3f-136">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no Clarizen é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="04d3f-136">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Clarizen is tooa user in Azure AD.</span></span> <span data-ttu-id="04d3f-137">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no Clarizen precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="04d3f-137">In other words, a link relationship between an Azure AD user and hello related user in Clarizen needs toobe established.</span></span> <span data-ttu-id="04d3f-138">Estabelecer essa relação de link atribuindo o valor de saudação do **nome de usuário** no AD do Azure como valor de saudação do **Username** no Clarizen.</span><span class="sxs-lookup"><span data-stu-id="04d3f-138">You establish this link relationship by assigning hello value of **user name** in Azure AD as hello value of **Username** in Clarizen.</span></span>

<span data-ttu-id="04d3f-139">tooconfigure e teste de logon único do AD do Azure com o Clarizen, Olá completa blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="04d3f-139">tooconfigure and test Azure AD single sign-on with Clarizen, complete hello following building blocks:</span></span>

1. <span data-ttu-id="04d3f-140">**[Configurar o logon único do AD do Azure](#configure-azure-ad-single-sign-on)**  tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="04d3f-140">**[Configure Azure AD single sign-on](#configure-azure-ad-single-sign-on)** tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="04d3f-141">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  tootest logon único do AD do Azure com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="04d3f-141">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="04d3f-142">**[Criar um usuário de teste do Clarizen](#create-a-clarizen-test-user)**  toohave um equivalente do Britta Simon no Clarizen é a representação toohello vinculado do Azure AD dela.</span><span class="sxs-lookup"><span data-stu-id="04d3f-142">**[Create a Clarizen test user](#create-a-clarizen-test-user)** toohave a counterpart of Britta Simon in Clarizen that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="04d3f-143">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="04d3f-143">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="04d3f-144">**[Testar o logon único](#test-single-sign-on)**  tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="04d3f-144">**[Test single sign-on](#test-single-sign-on)** tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="04d3f-145">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="04d3f-145">Configure Azure AD single sign-on</span></span>
<span data-ttu-id="04d3f-146">Habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Clarizen.</span><span class="sxs-lookup"><span data-stu-id="04d3f-146">Enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Clarizen application.</span></span>

1. <span data-ttu-id="04d3f-147">Em Olá portal do Azure, Olá **Clarizen** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-147">In hello Azure portal, on hello **Clarizen** application integration page, click **Single sign-on**.</span></span>

    ![Clicar em "Logon único"][4]

2. <span data-ttu-id="04d3f-149">Em Olá **o logon único** caixa de diálogo para **modo**, selecione **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="04d3f-149">In hello **Single sign-on** dialog box, for **Mode**, select **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Selecionar "Logon único baseado em SAML"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_01.png)

3. <span data-ttu-id="04d3f-151">Em Olá **Clarizen domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="04d3f-151">In hello **Clarizen Domain and URLs** section, perform hello following steps:</span></span>

    ![Caixas de URL de resposta e o identificador](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_02.png)

    <span data-ttu-id="04d3f-153">a.</span><span class="sxs-lookup"><span data-stu-id="04d3f-153">a.</span></span> <span data-ttu-id="04d3f-154">Em Olá **identificador** caixa, o valor do tipo hello como: **Clarizen**</span><span class="sxs-lookup"><span data-stu-id="04d3f-154">In hello **Identifier** box, type hello value as: **Clarizen**</span></span>

    <span data-ttu-id="04d3f-155">b.</span><span class="sxs-lookup"><span data-stu-id="04d3f-155">b.</span></span> <span data-ttu-id="04d3f-156">Em Olá **URL de resposta** , digite uma URL usando o saudação padrão a seguir: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span><span class="sxs-lookup"><span data-stu-id="04d3f-156">In hello **Reply URL** box, type a URL by using hello following pattern: **https://<company name>.clarizen.com/Clarizen/Pages/Integrations/SAML/SamlResponse.aspx**</span></span>

    > [!NOTE]
    > <span data-ttu-id="04d3f-157">Eles não são valores reais de saudação.</span><span class="sxs-lookup"><span data-stu-id="04d3f-157">These are not hello real values.</span></span> <span data-ttu-id="04d3f-158">Você tem toouse Olá real identificador e URL de resposta.</span><span class="sxs-lookup"><span data-stu-id="04d3f-158">You have toouse hello actual identifier and reply URL.</span></span> <span data-ttu-id="04d3f-159">Aqui, sugerimos que você use o valor exclusivo de saudação de uma cadeia de caracteres como Olá identificador.</span><span class="sxs-lookup"><span data-stu-id="04d3f-159">Here we suggest that you use hello unique value of a string as hello identifier.</span></span> <span data-ttu-id="04d3f-160">tooget Olá valores reais, Olá contato [equipe de suporte do Clarizen](https://success.clarizen.com/hc/en-us/requests/new).</span><span class="sxs-lookup"><span data-stu-id="04d3f-160">tooget hello actual values, contact hello [Clarizen support team](https://success.clarizen.com/hc/en-us/requests/new).</span></span>

4. <span data-ttu-id="04d3f-161">Em Olá **o certificado de autenticação SAML** seção, clique em **criar novo certificado**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-161">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Clicar em "Criar novo certificado"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_03.png)  

5. <span data-ttu-id="04d3f-163">Em Olá **criar um novo certificado** caixa de diálogo, clique o ícone de calendário hello e selecione uma data de expiração.</span><span class="sxs-lookup"><span data-stu-id="04d3f-163">In hello **Create New Certificate** dialog box, click hello calendar icon and select an expiry date.</span></span> <span data-ttu-id="04d3f-164">Em seguida, clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-164">Then click **Save**.</span></span>

    ![Selecionar e salvar uma data de expiração](./media/active-directory-saas-clarizen-tutorial/tutorial_general_300.png)

6. <span data-ttu-id="04d3f-166">Em Olá **o certificado de autenticação SAML** seção, selecione **ativar o novo certificado**e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-166">In hello **SAML Signing Certificate** section, select **Make new certificate active**, and then click **Save**.</span></span>

    ![Marcar Olá a caixa de seleção para tornar o novo certificado de saudação ativo](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_04.png)

7. <span data-ttu-id="04d3f-168">Em Olá **certificado de substituição** caixa de diálogo, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-168">In hello **Rollover certificate** dialog box, click **OK**.</span></span>

    ![Clicar em "Okey" tooconfirm que você deseja toomake Olá certificado active](./media/active-directory-saas-clarizen-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="04d3f-170">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="04d3f-170">In hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Clique em download de saudação toostart "Certificate (Base64)"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_05.png)

9. <span data-ttu-id="04d3f-172">Em Olá **Clarizen configuração** seção, clique em **configurar Clarizen** tooopen Olá **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="04d3f-172">In hello **Clarizen Configuration** section, click **Configure Clarizen** tooopen hello **Configure sign-on** window.</span></span>

    ![Clicar em "Configurar Clarizen"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_06.png)

    ![Janela "Configurar o logon", incluindo URLs e arquivos](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_07.png)

10. <span data-ttu-id="04d3f-175">Em uma janela de navegador web diferente, entre no site da empresa Clarizen tooyour como um administrador.</span><span class="sxs-lookup"><span data-stu-id="04d3f-175">In a different web browser window, sign in tooyour Clarizen company site as an administrator.</span></span>

11. <span data-ttu-id="04d3f-176">Clique no nome de usuário e em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-176">Click your username, and then click **Settings**.</span></span>

    <span data-ttu-id="04d3f-177">![Clicar em "Configurações" em seu nome de usuário](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="04d3f-177">![Clicking "Settings" under your username](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_001.png "Settings")</span></span>

12. <span data-ttu-id="04d3f-178">Clique em Olá **configurações globais** guia. Em seguida, Avançar muito**autenticação federada**, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-178">Click hello **Global Settings** tab. Then, next too**Federated Authentication**, click **edit**.</span></span>

    <span data-ttu-id="04d3f-179">![Guia "Configurações Globais"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Configurações Globais")</span><span class="sxs-lookup"><span data-stu-id="04d3f-179">!["Global Settings" tab](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_002.png "Global Settings")</span></span>

13. <span data-ttu-id="04d3f-180">Em Olá **autenticação federada** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="04d3f-180">In hello **Federated Authentication** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="04d3f-181">![Caixa de diálogo "Autenticação Federada"](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Autenticação Federada")</span><span class="sxs-lookup"><span data-stu-id="04d3f-181">!["Federated Authentication" dialog box](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_003.png "Federated Authentication")</span></span>

    <span data-ttu-id="04d3f-182">a.</span><span class="sxs-lookup"><span data-stu-id="04d3f-182">a.</span></span> <span data-ttu-id="04d3f-183">Selecione **Habilitar Autenticação Federada**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-183">Select **Enable Federated Authentication**.</span></span>

    <span data-ttu-id="04d3f-184">b.</span><span class="sxs-lookup"><span data-stu-id="04d3f-184">b.</span></span> <span data-ttu-id="04d3f-185">Clique em **carregar** tooupload seu certificado baixado.</span><span class="sxs-lookup"><span data-stu-id="04d3f-185">Click **Upload** tooupload your downloaded certificate.</span></span>

    <span data-ttu-id="04d3f-186">c.</span><span class="sxs-lookup"><span data-stu-id="04d3f-186">c.</span></span> <span data-ttu-id="04d3f-187">Em Olá **URL de entrada** , digite o valor de saudação do **Single Sign-On URL do serviço SAML** da janela de configuração de aplicativo de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="04d3f-187">In hello **Sign-in URL** box, enter hello value of **SAML Single Sign-On Service URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="04d3f-188">d.</span><span class="sxs-lookup"><span data-stu-id="04d3f-188">d.</span></span> <span data-ttu-id="04d3f-189">Em Olá **URL de logout** , digite o valor de saudação do **URL de logout** da janela de configuração de aplicativo de saudação do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="04d3f-189">In hello **Sign-out URL** box, enter hello value of **Sign-Out URL** from hello Azure AD application configuration window.</span></span>

    <span data-ttu-id="04d3f-190">e.</span><span class="sxs-lookup"><span data-stu-id="04d3f-190">e.</span></span> <span data-ttu-id="04d3f-191">Selecione **Usar POST**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-191">Select **Use POST**.</span></span>

    <span data-ttu-id="04d3f-192">f.</span><span class="sxs-lookup"><span data-stu-id="04d3f-192">f.</span></span> <span data-ttu-id="04d3f-193">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-193">Click **Save**.</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="04d3f-194">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="04d3f-194">Create an Azure AD test user</span></span>
<span data-ttu-id="04d3f-195">No portal do Azure de Olá, crie um usuário de teste chamado Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="04d3f-195">In hello Azure portal, create a test user called Britta Simon.</span></span>

![Nome e endereço de email do usuário de teste de saudação do AD do Azure][100]

1. <span data-ttu-id="04d3f-197">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="04d3f-197">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** icon.</span></span>

    ![Ícone do Azure Active Directory](./media/active-directory-saas-clarizen-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="04d3f-199">Clique em **usuários e grupos**e, em seguida, clique em **todos os usuários** toodisplay lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="04d3f-199">Click **Users and groups**, and then click **All users** toodisplay hello list of users.</span></span>

    ![Clicar em "Usuários e grupos" e "Todos os usuários"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="04d3f-201">Na parte superior de Olá Olá da caixa de diálogo, clique em **adicionar** tooopen Olá **usuário** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="04d3f-201">At hello top of hello dialog box, click **Add** tooopen hello **User** dialog box.</span></span>

    ![botão de "Adicionar" Hello](./media/active-directory-saas-clarizen-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="04d3f-203">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="04d3f-203">In hello **User** dialog box, perform hello following steps:</span></span>

    ![Caixa de diálogo "Usuário" com o nome, p endereço de email e a senha preenchidos](./media/active-directory-saas-clarizen-tutorial/create_aaduser_04.png)

    <span data-ttu-id="04d3f-205">a.</span><span class="sxs-lookup"><span data-stu-id="04d3f-205">a.</span></span> <span data-ttu-id="04d3f-206">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-206">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="04d3f-207">b.</span><span class="sxs-lookup"><span data-stu-id="04d3f-207">b.</span></span> <span data-ttu-id="04d3f-208">Em Olá **nome de usuário** caixa de endereço de email do tipo hello de saudação conta Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="04d3f-208">In hello **User name** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="04d3f-209">c.</span><span class="sxs-lookup"><span data-stu-id="04d3f-209">c.</span></span> <span data-ttu-id="04d3f-210">Selecione **Mostrar senha** e anote o valor de saudação do **senha**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-210">Select **Show Password** and write down hello value of **Password**.</span></span>

    <span data-ttu-id="04d3f-211">d.</span><span class="sxs-lookup"><span data-stu-id="04d3f-211">d.</span></span> <span data-ttu-id="04d3f-212">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-212">Click **Create**.</span></span>

### <a name="create-a-clarizen-test-user"></a><span data-ttu-id="04d3f-213">Criar um usuário de teste do Clarizen</span><span class="sxs-lookup"><span data-stu-id="04d3f-213">Create a Clarizen test user</span></span>
<span data-ttu-id="04d3f-214">tooenable a toosign de usuários do AD do Azure no tooClarizen, você deverá provisionar contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="04d3f-214">tooenable Azure AD users toosign in tooClarizen, you must provision user accounts.</span></span> <span data-ttu-id="04d3f-215">No caso de saudação do Clarizen, o provisionamento é uma tarefa manual.</span><span class="sxs-lookup"><span data-stu-id="04d3f-215">In hello case of Clarizen, provisioning is a manual task.</span></span>

1. <span data-ttu-id="04d3f-216">Entre no tooyour Clarizen site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="04d3f-216">Sign in tooyour Clarizen company site as an administrator.</span></span>

2. <span data-ttu-id="04d3f-217">Clique em **Pessoas**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-217">Click **People**.</span></span>

    <span data-ttu-id="04d3f-218">![Clicar em "Pessoas"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "Pessoas")</span><span class="sxs-lookup"><span data-stu-id="04d3f-218">![Clicking "People"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_001.png "People")</span></span>

3. <span data-ttu-id="04d3f-219">Clique em **Convidar Usuário**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-219">Click **Invite User**.</span></span>

    <span data-ttu-id="04d3f-220">![Botão "Convidar Usuário"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Convidar Usuários")</span><span class="sxs-lookup"><span data-stu-id="04d3f-220">!["Invite User" button](./media/active-directory-saas-clarizen-tutorial/create_aaduser_002.png "Invite Users")</span></span>

4. <span data-ttu-id="04d3f-221">Em Olá **convidar pessoas** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="04d3f-221">In hello **Invite People** dialog box, perform hello following steps:</span></span>

    <span data-ttu-id="04d3f-222">![Caixa de diálogo "Convidar Pessoas"](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Convidar Pessoas")</span><span class="sxs-lookup"><span data-stu-id="04d3f-222">!["Invite People" dialog box](./media/active-directory-saas-clarizen-tutorial/create_aaduser_003.png "Invite People")</span></span>

    <span data-ttu-id="04d3f-223">a.</span><span class="sxs-lookup"><span data-stu-id="04d3f-223">a.</span></span> <span data-ttu-id="04d3f-224">Em Olá **Email** caixa de endereço de email do tipo hello de saudação conta Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="04d3f-224">In hello **Email** box, type hello email address of hello Britta Simon account.</span></span>

    <span data-ttu-id="04d3f-225">b.</span><span class="sxs-lookup"><span data-stu-id="04d3f-225">b.</span></span> <span data-ttu-id="04d3f-226">Clique em **Convidar**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-226">Click **Invite**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="04d3f-227">proprietário de conta do Active Directory do Azure Olá será receberá um email e execute tooconfirm um link em sua conta antes de se tornar ativa.</span><span class="sxs-lookup"><span data-stu-id="04d3f-227">hello Azure Active Directory account holder will receive an email and follow a link tooconfirm their account before it becomes active.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="04d3f-228">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="04d3f-228">Assign hello Azure AD test user</span></span>
<span data-ttu-id="04d3f-229">Habilite Britta Simon toouse logon único do Azure, concedendo tooClarizen seu acesso.</span><span class="sxs-lookup"><span data-stu-id="04d3f-229">Enable Britta Simon toouse Azure single sign-on by granting her access tooClarizen.</span></span>

![Usuário de teste atribuído][200]

1. <span data-ttu-id="04d3f-231">No portal do Azure de Olá, abrir modo de exibição de aplicativos de saudação, toohello directory modo de navegação, clique em **aplicativos empresariais**e, em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-231">In hello Azure portal, open hello applications view, browse toohello directory view, click **Enterprise applications**, and then click **All applications**.</span></span>

    ![Clicar em "Aplicativos corporativos" e em "Todos os aplicativos"][201]

2. <span data-ttu-id="04d3f-233">Na lista de aplicativos hello, selecione **Clarizen**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-233">In hello applications list, select **Clarizen**.</span></span>

    ![Selecionando Clarizen na lista de saudação](./media/active-directory-saas-clarizen-tutorial/tutorial_clarizen_50.png)

3. <span data-ttu-id="04d3f-235">No painel esquerdo do hello, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-235">In hello left pane, click **Users and groups**.</span></span>

    ![Clicar em “Usuário e grupos”][202]

4. <span data-ttu-id="04d3f-237">Clique em Olá **adicionar** botão.</span><span class="sxs-lookup"><span data-stu-id="04d3f-237">Click hello **Add** button.</span></span> <span data-ttu-id="04d3f-238">Em seguida, no hello **Adicionar atribuição** caixa de diálogo, selecione **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="04d3f-238">Then, in hello **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![botão de "Adicionar" Hello e caixa de diálogo "Adicionar atribuição" hello][203]

5. <span data-ttu-id="04d3f-240">Em Olá **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de saudação de usuários.</span><span class="sxs-lookup"><span data-stu-id="04d3f-240">In hello **Users and groups** dialog box, select **Britta Simon** in hello list of users.</span></span>

6. <span data-ttu-id="04d3f-241">Em Olá **usuários e grupos** caixa de diálogo, clique em Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="04d3f-241">In hello **Users and groups** dialog box, click hello **Select** button.</span></span>

7. <span data-ttu-id="04d3f-242">Em Olá **Adicionar atribuição** caixa de diálogo, clique em Olá **atribuir** botão.</span><span class="sxs-lookup"><span data-stu-id="04d3f-242">In hello **Add Assignment** dialog box, click hello **Assign** button.</span></span>

### <a name="test-single-sign-on"></a><span data-ttu-id="04d3f-243">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="04d3f-243">Test single sign-on</span></span>
<span data-ttu-id="04d3f-244">Teste sua configuração do Azure AD único logon usando Olá painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="04d3f-244">Test your Azure AD single sign-on configuration by using hello Access Panel.</span></span>

<span data-ttu-id="04d3f-245">Quando você clica em bloco Clarizen Olá Olá painel de acesso, você deve ser conectado automaticamente tooyour aplicativo Clarizen.</span><span class="sxs-lookup"><span data-stu-id="04d3f-245">When you click hello Clarizen tile in hello Access Panel, you should be automatically signed in tooyour Clarizen application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="04d3f-246">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="04d3f-246">Additional resources</span></span>

* [<span data-ttu-id="04d3f-247">Lista de tutoriais sobre como aplicativos de SaaS toointegrate com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="04d3f-247">List of tutorials on how toointegrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="04d3f-248">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="04d3f-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clarizen-tutorial/tutorial_general_203.png
