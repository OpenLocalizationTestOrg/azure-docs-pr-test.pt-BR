---
title: "Tutorial: Integração do Azure Active Directory com o RealtimeBoard | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e RealtimeBoard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a37fc1c0-4bae-4173-989b-00de53a0076f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: jeedes
ms.openlocfilehash: 76644c9ba643d61a903295dea4d417716a47774a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-realtimeboard"></a><span data-ttu-id="10980-103">Tutorial: Integração do Azure Active Directory com o RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="10980-103">Tutorial: Azure Active Directory integration with RealtimeBoard</span></span>

<span data-ttu-id="10980-104">Neste tutorial, você aprenderá como toointegrate RealtimeBoard com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="10980-104">In this tutorial, you learn how toointegrate RealtimeBoard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="10980-105">Integrando RealtimeBoard com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="10980-105">Integrating RealtimeBoard with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="10980-106">Você pode controlar no AD do Azure que tenha acesso tooRealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="10980-106">You can control in Azure AD who has access tooRealtimeBoard.</span></span>
- <span data-ttu-id="10980-107">Você pode habilitar seu usuários tooautomatically get conectado tooRealtimeBoard (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="10980-107">You can enable your users tooautomatically get signed-on tooRealtimeBoard (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="10980-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="10980-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="10980-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="10980-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10980-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="10980-110">Prerequisites</span></span>

<span data-ttu-id="10980-111">tooconfigure integração do AD do Azure com RealtimeBoard, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="10980-111">tooconfigure Azure AD integration with RealtimeBoard, you need hello following items:</span></span>

- <span data-ttu-id="10980-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10980-112">An Azure AD subscription</span></span>
- <span data-ttu-id="10980-113">Uma assinatura habilitada para logon único do RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="10980-113">A RealtimeBoard single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="10980-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="10980-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="10980-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="10980-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="10980-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="10980-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="10980-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="10980-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="10980-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="10980-118">Scenario description</span></span>
<span data-ttu-id="10980-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="10980-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="10980-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="10980-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="10980-121">Adicionando RealtimeBoard da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="10980-121">Adding RealtimeBoard from hello gallery</span></span>
2. <span data-ttu-id="10980-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10980-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-realtimeboard-from-hello-gallery"></a><span data-ttu-id="10980-123">Adicionando RealtimeBoard da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="10980-123">Adding RealtimeBoard from hello gallery</span></span>
<span data-ttu-id="10980-124">integração de saudação tooconfigure de RealtimeBoard no AD do Azure, você precisa tooadd RealtimeBoard da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="10980-124">tooconfigure hello integration of RealtimeBoard into Azure AD, you need tooadd RealtimeBoard from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="10980-125">**tooadd RealtimeBoard da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="10980-125">**tooadd RealtimeBoard from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="10980-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="10980-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="10980-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="10980-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="10980-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="10980-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="10980-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="10980-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="10980-133">Na caixa de pesquisa hello, digite **RealtimeBoard**, selecione **RealtimeBoard** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="10980-133">In hello search box, type **RealtimeBoard**, select **RealtimeBoard** from result panel then click **Add** button tooadd hello application.</span></span>

    ![RealtimeBoard na lista de resultados de saudação](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="10980-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="10980-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="10980-136">Nesta seção, você vai configurar e testar o logon único do Azure AD com o RealtimeBoard com base em um usuário de teste chamado "Brenda Fernandes".</span><span class="sxs-lookup"><span data-stu-id="10980-136">In this section, you configure and test Azure AD single sign-on with RealtimeBoard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="10980-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em RealtimeBoard é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="10980-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in RealtimeBoard is tooa user in Azure AD.</span></span> <span data-ttu-id="10980-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em RealtimeBoard precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="10980-138">In other words, a link relationship between an Azure AD user and hello related user in RealtimeBoard needs toobe established.</span></span>

<span data-ttu-id="10980-139">RealtimeBoard, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="10980-139">In RealtimeBoard, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="10980-140">tooconfigure e teste de logon único do AD do Azure com RealtimeBoard, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="10980-140">tooconfigure and test Azure AD single sign-on with RealtimeBoard, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="10980-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="10980-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="10980-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="10980-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="10980-143">**[Criar um usuário de teste RealtimeBoard](#create-a-realtimeboard-test-user)**  -toohave um equivalente do Britta Simon em RealtimeBoard é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="10980-143">**[Create a RealtimeBoard test user](#create-a-realtimeboard-test-user)** - toohave a counterpart of Britta Simon in RealtimeBoard that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="10980-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="10980-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="10980-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="10980-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="10980-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="10980-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="10980-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="10980-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your RealtimeBoard application.</span></span>

<span data-ttu-id="10980-148">**tooconfigure AD do Azure-logon único com RealtimeBoard, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="10980-148">**tooconfigure Azure AD single sign-on with RealtimeBoard, perform hello following steps:**</span></span>

1. <span data-ttu-id="10980-149">Em Olá portal do Azure, Olá **RealtimeBoard** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="10980-149">In hello Azure portal, on hello **RealtimeBoard** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="10980-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="10980-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_samlbase.png)

3. <span data-ttu-id="10980-153">Em Olá **RealtimeBoard domínio e URLs** seção, se desejar que o aplicativo hello tooconfigure **IDP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="10980-153">On hello **RealtimeBoard Domain and URLs** section, if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Informações de logon único em Domínio e URLs do RealtimeBoard](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url.png)

    <span data-ttu-id="10980-155">Em Olá **identificador** caixa de texto, digite um URL como:`https://realtimeboard.com/`</span><span class="sxs-lookup"><span data-stu-id="10980-155">In hello **Identifier** textbox, type a URL as: `https://realtimeboard.com/`</span></span>

4. <span data-ttu-id="10980-156">Verificar **Mostrar configurações de URL avançadas**, se desejar que o aplicativo hello tooconfigure **SP** modo iniciado:</span><span class="sxs-lookup"><span data-stu-id="10980-156">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url2.png)

    <span data-ttu-id="10980-158">Em Olá **URL de logon** caixa de texto, digite um URL como:`https://realtimeboard.com/sso/saml`</span><span class="sxs-lookup"><span data-stu-id="10980-158">In hello **Sign-on URL** textbox, type a URL as: `https://realtimeboard.com/sso/saml`</span></span>

5. <span data-ttu-id="10980-159">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo de metadados de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="10980-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_certificate.png) 

6. <span data-ttu-id="10980-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="10980-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="10980-163">tooconfigure logon único no **RealtimeBoard** lado, você precisa toosend Olá baixado **Metadata XML** muito[a equipe de suporte RealtimeBoard](mailto:support@realtimeboard.com).</span><span class="sxs-lookup"><span data-stu-id="10980-163">tooconfigure single sign-on on **RealtimeBoard** side, you need toosend hello downloaded **Metadata XML** too[RealtimeBoard support team](mailto:support@realtimeboard.com).</span></span> <span data-ttu-id="10980-164">Eles definidos Olá de toohave essa configuração conexão SSO do SAML definido corretamente em ambos os lados.</span><span class="sxs-lookup"><span data-stu-id="10980-164">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="10980-165">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="10980-165">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="10980-166">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="10980-166">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="10980-167">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="10980-167">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="10980-168">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="10980-168">Create an Azure AD test user</span></span>

<span data-ttu-id="10980-169">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="10980-169">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="10980-171">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="10980-171">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="10980-172">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="10980-172">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="10980-174">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="10980-174">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="10980-176">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="10980-176">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="10980-178">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="10980-178">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_04.png)

    <span data-ttu-id="10980-180">a.</span><span class="sxs-lookup"><span data-stu-id="10980-180">a.</span></span> <span data-ttu-id="10980-181">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="10980-181">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="10980-182">b.</span><span class="sxs-lookup"><span data-stu-id="10980-182">b.</span></span> <span data-ttu-id="10980-183">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="10980-183">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="10980-184">c.</span><span class="sxs-lookup"><span data-stu-id="10980-184">c.</span></span> <span data-ttu-id="10980-185">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="10980-185">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="10980-186">d.</span><span class="sxs-lookup"><span data-stu-id="10980-186">d.</span></span> <span data-ttu-id="10980-187">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="10980-187">Click **Create**.</span></span>
 
### <a name="create-a-realtimeboard-test-user"></a><span data-ttu-id="10980-188">Criar um usuário de teste do RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="10980-188">Create a RealtimeBoard test user</span></span>

<span data-ttu-id="10980-189">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="10980-189">hello objective of this section is toocreate a user called Britta Simon in RealtimeBoard.</span></span> <span data-ttu-id="10980-190">O RealtimeBoard dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="10980-190">RealtimeBoard supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="10980-191">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="10980-191">There is no action item for you in this section.</span></span> <span data-ttu-id="10980-192">Se um usuário ainda não existir na RealtimeBoard, um novo será criado quando você tenta tooaccess RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="10980-192">If a user doesn't already exist in RealtimeBoard, a new one is created when you attempt tooaccess RealtimeBoard.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="10980-193">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="10980-193">Assign hello Azure AD test user</span></span>

<span data-ttu-id="10980-194">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooRealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="10980-194">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooRealtimeBoard.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="10980-196">**tooassign Britta Simon tooRealtimeBoard, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="10980-196">**tooassign Britta Simon tooRealtimeBoard, perform hello following steps:**</span></span>

1. <span data-ttu-id="10980-197">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="10980-197">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="10980-199">Na lista de aplicativos hello, selecione **RealtimeBoard**.</span><span class="sxs-lookup"><span data-stu-id="10980-199">In hello applications list, select **RealtimeBoard**.</span></span>

    ![link de RealtimeBoard Olá na lista de aplicativos Olá](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_app.png)  

3. <span data-ttu-id="10980-201">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="10980-201">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="10980-203">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="10980-203">Click **Add** button.</span></span> <span data-ttu-id="10980-204">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="10980-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="10980-206">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="10980-206">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="10980-207">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="10980-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="10980-208">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="10980-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="10980-209">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="10980-209">Test single sign-on</span></span>

<span data-ttu-id="10980-210">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="10980-210">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="10980-211">Quando você clica em bloco RealtimeBoard Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour RealtimeBoard aplicativo.</span><span class="sxs-lookup"><span data-stu-id="10980-211">When you click hello RealtimeBoard tile in hello Access Panel, you should get automatically signed-on tooyour RealtimeBoard application.</span></span>
<span data-ttu-id="10980-212">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="10980-212">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="10980-213">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="10980-213">Additional resources</span></span>

* [<span data-ttu-id="10980-214">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="10980-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="10980-215">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="10980-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_203.png

