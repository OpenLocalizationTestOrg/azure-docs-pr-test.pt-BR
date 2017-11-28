---
title: "Tutorial: Integração do Azure Active Directory com o LogicMonitor | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e LogicMonitor."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 496156c3-0e22-4492-b36f-2c29c055e087
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: ea5cb8b574d763cb114286e3b2a5c94ab5546756
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-logicmonitor"></a><span data-ttu-id="e9ad0-103">Tutorial: Integração do Active Directory do Azure com o LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="e9ad0-103">Tutorial: Azure Active Directory integration with LogicMonitor</span></span>

<span data-ttu-id="e9ad0-104">Neste tutorial, você aprenderá como toointegrate LogicMonitor com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="e9ad0-104">In this tutorial, you learn how toointegrate LogicMonitor with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9ad0-105">Integrando o LogicMonitor com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9ad0-105">Integrating LogicMonitor with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e9ad0-106">Você pode controlar no AD do Azure que tenha acesso tooLogicMonitor</span><span class="sxs-lookup"><span data-stu-id="e9ad0-106">You can control in Azure AD who has access tooLogicMonitor</span></span>
- <span data-ttu-id="e9ad0-107">Você pode habilitar seu usuários tooautomatically get conectado tooLogicMonitor (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e9ad0-107">You can enable your users tooautomatically get signed-on tooLogicMonitor (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e9ad0-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e9ad0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e9ad0-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9ad0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9ad0-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e9ad0-110">Prerequisites</span></span>

<span data-ttu-id="e9ad0-111">tooconfigure integração do AD do Azure com LogicMonitor, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9ad0-111">tooconfigure Azure AD integration with LogicMonitor, you need hello following items:</span></span>

- <span data-ttu-id="e9ad0-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e9ad0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9ad0-113">Uma assinatura habilitada para logon único do LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="e9ad0-113">A LogicMonitor single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9ad0-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e9ad0-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="e9ad0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9ad0-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e9ad0-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9ad0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9ad0-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="e9ad0-118">Scenario description</span></span>
<span data-ttu-id="e9ad0-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9ad0-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="e9ad0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9ad0-121">Adicionando LogicMonitor da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ad0-121">Adding LogicMonitor from hello gallery</span></span>
2. <span data-ttu-id="e9ad0-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e9ad0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-logicmonitor-from-hello-gallery"></a><span data-ttu-id="e9ad0-123">Adicionando LogicMonitor da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="e9ad0-123">Adding LogicMonitor from hello gallery</span></span>
<span data-ttu-id="e9ad0-124">integração de saudação tooconfigure do LogicMonitor no AD do Azure, você precisa tooadd LogicMonitor da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-124">tooconfigure hello integration of LogicMonitor into Azure AD, you need tooadd LogicMonitor from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e9ad0-125">**tooadd LogicMonitor da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e9ad0-125">**tooadd LogicMonitor from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9ad0-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e9ad0-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e9ad0-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="e9ad0-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="e9ad0-133">Na caixa de pesquisa hello, digite **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-133">In hello search box, type **LogicMonitor**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_search.png)

5. <span data-ttu-id="e9ad0-135">No painel de resultados de saudação, selecione **LogicMonitor**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-135">In hello results panel, select **LogicMonitor**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e9ad0-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e9ad0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e9ad0-138">Nesta seção, você configurará e testará o logon único do Azure AD com o LogicMonitor, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-138">In this section, you configure and test Azure AD single sign-on with LogicMonitor based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e9ad0-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá no LogicMonitor é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LogicMonitor is tooa user in Azure AD.</span></span> <span data-ttu-id="e9ad0-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação no LogicMonitor precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-140">In other words, a link relationship between an Azure AD user and hello related user in LogicMonitor needs toobe established.</span></span>

<span data-ttu-id="e9ad0-141">No LogicMonitor, atribuir o valor de saudação do hello **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-141">In LogicMonitor, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e9ad0-142">tooconfigure e teste de logon único do AD do Azure com LogicMonitor, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9ad0-142">tooconfigure and test Azure AD single sign-on with LogicMonitor, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e9ad0-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e9ad0-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9ad0-145">**[Criar um usuário de teste do LogicMonitor](#creating-a-logicmonitor-test-user)**  -toohave um equivalente do Britta Simon no LogicMonitor é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-145">**[Creating a LogicMonitor test user](#creating-a-logicmonitor-test-user)** - toohave a counterpart of Britta Simon in LogicMonitor that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e9ad0-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9ad0-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e9ad0-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9ad0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e9ad0-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo do LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your LogicMonitor application.</span></span>

<span data-ttu-id="e9ad0-150">**tooconfigure AD do Azure-logon único com LogicMonitor, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e9ad0-150">**tooconfigure Azure AD single sign-on with LogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9ad0-151">Em Olá portal do Azure, Olá **LogicMonitor** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-151">In hello Azure portal, on hello **LogicMonitor** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="e9ad0-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_samlbase.png)

3. <span data-ttu-id="e9ad0-155">Em Olá **LogicMonitor domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9ad0-155">On hello **LogicMonitor Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_url.png)

    <span data-ttu-id="e9ad0-157">a.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-157">a.</span></span> <span data-ttu-id="e9ad0-158">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="e9ad0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    <span data-ttu-id="e9ad0-159">b.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-159">b.</span></span> <span data-ttu-id="e9ad0-160">Em Olá **identificador** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<companyname>.logicmonitor.com`</span><span class="sxs-lookup"><span data-stu-id="e9ad0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.logicmonitor.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e9ad0-161">Esses valores não são reais.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-161">These values are not real.</span></span> <span data-ttu-id="e9ad0-162">Atualizar esses valores com hello real URL de logon e o identificador.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e9ad0-163">Entre em contato com [equipe de suporte do cliente LogicMonitor](https://www.logicmonitor.com/contact/) tooget esses valores.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-163">Contact [LogicMonitor Client support team](https://www.logicmonitor.com/contact/) tooget these values.</span></span> 
 


4. <span data-ttu-id="e9ad0-164">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_certificate.png) 

5. <span data-ttu-id="e9ad0-166">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="e9ad0-166">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e9ad0-168">Faça logon no tooyour **LogicMonitor** site da empresa como um administrador.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-168">Log in tooyour **LogicMonitor** company site as an administrator.</span></span>

7. <span data-ttu-id="e9ad0-169">No menu de saudação na parte superior de saudação, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-169">In hello menu on hello top, click **Settings**.</span></span>
   
   <span data-ttu-id="e9ad0-170">![Configurações](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Configurações")</span><span class="sxs-lookup"><span data-stu-id="e9ad0-170">![Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790052.png "Settings")</span></span>

8. <span data-ttu-id="e9ad0-171">No hello bat de navegação no lado esquerdo do hello, clique em **logon único**</span><span class="sxs-lookup"><span data-stu-id="e9ad0-171">In hello navigation bat on hello left side, click **Single Sign On**</span></span>
   
   <span data-ttu-id="e9ad0-172">![Logon Único](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Logon Único")</span><span class="sxs-lookup"><span data-stu-id="e9ad0-172">![Single Sign-On](./media/active-directory-saas-logicmonitor-tutorial/ic790053.png "Single Sign-On")</span></span>

9. <span data-ttu-id="e9ad0-173">Em Olá **as configurações de logon único (SSO)** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9ad0-173">In hello **Single Sign-on (SSO) settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="e9ad0-174">![Configurações de Logon Único](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Configurações de Logon Único")</span><span class="sxs-lookup"><span data-stu-id="e9ad0-174">![Single Sign-On Settings](./media/active-directory-saas-logicmonitor-tutorial/ic790054.png "Single Sign-On Settings")</span></span>
   
   <span data-ttu-id="e9ad0-175">a.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-175">a.</span></span> <span data-ttu-id="e9ad0-176">Selecione **Habilitar Logon Único**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-176">Select **Enable Single Sign-on**.</span></span>

   <span data-ttu-id="e9ad0-177">b.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-177">b.</span></span> <span data-ttu-id="e9ad0-178">Para **Atribuição de Função Padrão**, selecione **readonly**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-178">As **Default Role Assignment**, select **readonly**.</span></span>
   
   <span data-ttu-id="e9ad0-179">c.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-179">c.</span></span> <span data-ttu-id="e9ad0-180">Abra o arquivo de metadados de saudação baixado no bloco de notas e, em seguida, cole o conteúdo do arquivo hello Olá **metadados do provedor de identidade** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-180">Open hello downloaded metadata file in notepad, and then paste content of hello file into hello **Identity Provider Metadata** textbox.</span></span>
   
   <span data-ttu-id="e9ad0-181">d.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-181">d.</span></span> <span data-ttu-id="e9ad0-182">Clique em **Salvar Alterações**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-182">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="e9ad0-183">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="e9ad0-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e9ad0-184">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e9ad0-185">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e9ad0-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e9ad0-186">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e9ad0-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="e9ad0-187">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="e9ad0-189">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e9ad0-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9ad0-190">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e9ad0-192">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e9ad0-194">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e9ad0-196">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9ad0-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-logicmonitor-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e9ad0-198">a.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-198">a.</span></span> <span data-ttu-id="e9ad0-199">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9ad0-200">b.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-200">b.</span></span> <span data-ttu-id="e9ad0-201">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e9ad0-202">c.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-202">c.</span></span> <span data-ttu-id="e9ad0-203">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e9ad0-204">d.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-204">d.</span></span> <span data-ttu-id="e9ad0-205">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-205">Click **Create**.</span></span>
 
### <a name="creating-a-logicmonitor-test-user"></a><span data-ttu-id="e9ad0-206">Criar um usuário de teste do LogicMonitor</span><span class="sxs-lookup"><span data-stu-id="e9ad0-206">Creating a LogicMonitor test user</span></span>

<span data-ttu-id="e9ad0-207">Para AAD usuários toobe capaz de toosign no, eles devem ser provisionado toohello aplicativo do LogicMonitor usando seus nomes de usuário do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-207">For AAD users toobe able toosign in, they must be provisioned toohello LogicMonitor application using their Azure Active Directory user names.</span></span>

<span data-ttu-id="e9ad0-208">**tooconfigure provisionamento de usuário, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e9ad0-208">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9ad0-209">Faça logon no tooyour site da empresa LogicMonitor como um administrador.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-209">Log in tooyour LogicMonitor company site as an administrator.</span></span>

2. <span data-ttu-id="e9ad0-210">No menu de saudação na parte superior de saudação, clique em **configurações**e, em seguida, clique em **funções e usuários**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-210">In hello menu on hello top, click **Settings**, and then click **Roles and Users**.</span></span>
   
   <span data-ttu-id="e9ad0-211">![Funções e Usuários](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Funções e Usuários")</span><span class="sxs-lookup"><span data-stu-id="e9ad0-211">![Roles and Users](./media/active-directory-saas-logicmonitor-tutorial/ic790056.png "Roles and Users")</span></span>

3. <span data-ttu-id="e9ad0-212">Clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-212">Click **Add**.</span></span>

4. <span data-ttu-id="e9ad0-213">Em Olá **adicionar uma conta** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e9ad0-213">In hello **Add an account** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="e9ad0-214">![Adicionar uma conta](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Adicionar uma conta")</span><span class="sxs-lookup"><span data-stu-id="e9ad0-214">![Add an account](./media/active-directory-saas-logicmonitor-tutorial/ic790057.png "Add an account")</span></span>
   
   <span data-ttu-id="e9ad0-215">a.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-215">a.</span></span> <span data-ttu-id="e9ad0-216">Saudação de tipo **Username**, **Email**, **senha**, e **senha Insira novamente** valores de usuário do Active Directory do Azure Olá desejado tooprovision em Olá relacionados caixas de texto.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-216">Type hello **Username**, **Email**, **Password**, and **Retype password** values of hello Azure Active Directory user you want tooprovision into hello related textboxes.</span></span>
   
   <span data-ttu-id="e9ad0-217">b.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-217">b.</span></span> <span data-ttu-id="e9ad0-218">Selecione **funções**, **permissões de exibição**e hello **Status**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-218">Select **Roles**, **View Permissions**, and hello **Status**.</span></span>
   
   <span data-ttu-id="e9ad0-219">c.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-219">c.</span></span> <span data-ttu-id="e9ad0-220">Clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-220">Click **Submit**.</span></span>

>[!NOTE]
><span data-ttu-id="e9ad0-221">Você pode usar qualquer ferramenta de criação outros LogicMonitor usuário conta ou APIs fornecidas pelo LogicMonitor tooprovision Azure Active Directory as contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-221">You can use any other LogicMonitor user account creation tools or APIs provided by LogicMonitor tooprovision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e9ad0-222">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="e9ad0-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e9ad0-223">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooLogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLogicMonitor.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="e9ad0-225">**tooassign Britta Simon tooLogicMonitor, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="e9ad0-225">**tooassign Britta Simon tooLogicMonitor, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9ad0-226">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="e9ad0-228">Na lista de aplicativos hello, selecione **LogicMonitor**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-228">In hello applications list, select **LogicMonitor**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-logicmonitor-tutorial/tutorial_logicmonitor_app.png) 

3. <span data-ttu-id="e9ad0-230">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="e9ad0-232">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-232">Click **Add** button.</span></span> <span data-ttu-id="e9ad0-233">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="e9ad0-235">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e9ad0-236">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e9ad0-237">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e9ad0-238">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="e9ad0-238">Testing single sign-on</span></span>

<span data-ttu-id="e9ad0-239">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
 
<span data-ttu-id="e9ad0-240">Quando você clica em bloco LogicMonitor Olá Olá painel de acesso, você deve obter tooyour automaticamente conectado no aplicativo do LogicMonitor.</span><span class="sxs-lookup"><span data-stu-id="e9ad0-240">When you click hello LogicMonitor tile in hello Access Panel, you should get automatically signed-on tooyour LogicMonitor application.</span></span>
<span data-ttu-id="e9ad0-241">Para obter mais informações sobre Olá painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e9ad0-241">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e9ad0-242">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e9ad0-242">Additional resources</span></span>

* [<span data-ttu-id="e9ad0-243">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="e9ad0-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9ad0-244">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e9ad0-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-logicmonitor-tutorial/tutorial_general_203.png

