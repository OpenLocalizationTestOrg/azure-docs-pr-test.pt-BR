---
title: "Tutorial: Integração do Azure Active Directory com o Workrite | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e Workrite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: a663374ae3c8b102b53d8cf05a9cb083b80dbb83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="47656-103">Tutorial: Integração do Active Directory do Azure com o Workrite</span><span class="sxs-lookup"><span data-stu-id="47656-103">Tutorial: Azure Active Directory integration with Workrite</span></span>

<span data-ttu-id="47656-104">Neste tutorial, você aprenderá como toointegrate Workrite com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="47656-104">In this tutorial, you learn how toointegrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="47656-105">Integrando Workrite com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="47656-105">Integrating Workrite with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="47656-106">Você pode controlar no AD do Azure que tenha acesso tooWorkrite.</span><span class="sxs-lookup"><span data-stu-id="47656-106">You can control in Azure AD who has access tooWorkrite.</span></span>
- <span data-ttu-id="47656-107">Você pode habilitar seu usuários tooautomatically get conectado tooWorkrite (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="47656-107">You can enable your users tooautomatically get signed-on tooWorkrite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="47656-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="47656-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="47656-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="47656-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47656-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="47656-110">Prerequisites</span></span>

<span data-ttu-id="47656-111">tooconfigure integração do AD do Azure com Workrite, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="47656-111">tooconfigure Azure AD integration with Workrite, you need hello following items:</span></span>

- <span data-ttu-id="47656-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="47656-112">An Azure AD subscription</span></span>
- <span data-ttu-id="47656-113">Uma assinatura do Workrite habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="47656-113">A Workrite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="47656-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="47656-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="47656-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="47656-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="47656-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="47656-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="47656-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="47656-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="47656-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="47656-118">Scenario description</span></span>
<span data-ttu-id="47656-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="47656-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="47656-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="47656-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="47656-121">Adicionando Workrite da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="47656-121">Adding Workrite from hello gallery</span></span>
2. <span data-ttu-id="47656-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="47656-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workrite-from-hello-gallery"></a><span data-ttu-id="47656-123">Adicionando Workrite da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="47656-123">Adding Workrite from hello gallery</span></span>
<span data-ttu-id="47656-124">integração de saudação tooconfigure de Workrite no AD do Azure, você precisa tooadd Workrite da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="47656-124">tooconfigure hello integration of Workrite into Azure AD, you need tooadd Workrite from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="47656-125">**tooadd Workrite da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="47656-125">**tooadd Workrite from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="47656-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="47656-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="47656-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="47656-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="47656-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="47656-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="47656-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="47656-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="47656-133">Na caixa de pesquisa hello, digite **Workrite**, selecione **Workrite** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="47656-133">In hello search box, type **Workrite**, select **Workrite** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Workrite na lista de resultados de saudação](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="47656-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="47656-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="47656-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Workrite com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="47656-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="47656-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em Workrite é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="47656-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Workrite is tooa user in Azure AD.</span></span> <span data-ttu-id="47656-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em Workrite precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="47656-138">In other words, a link relationship between an Azure AD user and hello related user in Workrite needs toobe established.</span></span>

<span data-ttu-id="47656-139">Workrite, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="47656-139">In Workrite, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="47656-140">tooconfigure e teste de logon único do AD do Azure com Workrite, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="47656-140">tooconfigure and test Azure AD single sign-on with Workrite, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="47656-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="47656-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="47656-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47656-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="47656-143">**[Criar um usuário de teste Workrite](#create-a-workrite-test-user)**  -toohave um equivalente do Britta Simon em Workrite é toohello vinculado do Azure AD representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="47656-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - toohave a counterpart of Britta Simon in Workrite that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="47656-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="47656-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="47656-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="47656-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="47656-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="47656-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="47656-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo Workrite.</span><span class="sxs-lookup"><span data-stu-id="47656-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Workrite application.</span></span>

<span data-ttu-id="47656-148">**tooconfigure AD do Azure-logon único com Workrite, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="47656-148">**tooconfigure Azure AD single sign-on with Workrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="47656-149">Em Olá portal do Azure, Olá **Workrite** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="47656-149">In hello Azure portal, on hello **Workrite** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="47656-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="47656-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_samlbase.png)

3. <span data-ttu-id="47656-153">Em Olá **Workrite domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="47656-153">On hello **Workrite Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de URLs e Domínio do Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_url.png)

    <span data-ttu-id="47656-155">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="47656-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="47656-156">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="47656-156">This value is not real.</span></span> <span data-ttu-id="47656-157">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="47656-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="47656-158">Entre em contato com [equipe de suporte do cliente Workrite](mailto:support@workrite.co.uk) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="47656-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) tooget this value.</span></span>

4. <span data-ttu-id="47656-159">Em Olá **o certificado de autenticação SAML** seção, clique em **Certificate(Base64)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="47656-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_certificate.png) 

5. <span data-ttu-id="47656-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="47656-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-workrite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="47656-163">Em Olá **Workrite configuração** seção, clique em **configurar Workrite** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="47656-163">On hello **Workrite Configuration** section, click **Configure Workrite** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="47656-164">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="47656-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_configure.png) 

7. <span data-ttu-id="47656-166">tooconfigure logon único no **Workrite** lado, você precisa toosend Olá baixado **Certificate(Base64), URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** muito[Workrite equipe de suporte](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="47656-166">tooconfigure single sign-on on **Workrite** side, you need toosend hello downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Workrite support team](mailto:support@workrite.co.uk).</span></span>

> [!TIP]
> <span data-ttu-id="47656-167">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="47656-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="47656-168">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="47656-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="47656-169">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="47656-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="47656-170">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="47656-170">Create an Azure AD test user</span></span>

<span data-ttu-id="47656-171">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="47656-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="47656-173">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="47656-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="47656-174">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="47656-174">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-workrite-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="47656-176">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="47656-176">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-workrite-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="47656-178">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="47656-178">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-workrite-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="47656-180">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="47656-180">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-workrite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="47656-182">a.</span><span class="sxs-lookup"><span data-stu-id="47656-182">a.</span></span> <span data-ttu-id="47656-183">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="47656-183">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="47656-184">b.</span><span class="sxs-lookup"><span data-stu-id="47656-184">b.</span></span> <span data-ttu-id="47656-185">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="47656-185">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="47656-186">c.</span><span class="sxs-lookup"><span data-stu-id="47656-186">c.</span></span> <span data-ttu-id="47656-187">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="47656-187">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="47656-188">d.</span><span class="sxs-lookup"><span data-stu-id="47656-188">d.</span></span> <span data-ttu-id="47656-189">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="47656-189">Click **Create**.</span></span>
 
### <a name="create-a-workrite-test-user"></a><span data-ttu-id="47656-190">Criar um usuário de teste do Workrite</span><span class="sxs-lookup"><span data-stu-id="47656-190">Create a Workrite test user</span></span>

<span data-ttu-id="47656-191">Olá objetivo desta seção é toocreate um usuário chamado Britta Simon no Workrite.</span><span class="sxs-lookup"><span data-stu-id="47656-191">hello objective of this section is toocreate a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="47656-192">**toocreate um usuário chamado Britta Simon no Workrite, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="47656-192">**toocreate a user called Britta Simon in Workrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="47656-193">Faça logon no site da empresa workrite tooyour como administrador.</span><span class="sxs-lookup"><span data-stu-id="47656-193">Sign on tooyour workrite company site as administrator.</span></span>

2. <span data-ttu-id="47656-194">No painel de navegação de saudação, clique em **Admin**.</span><span class="sxs-lookup"><span data-stu-id="47656-194">In hello navigation pane, click **Admin**.</span></span>
   
    ![Controle de administração][400]

3. <span data-ttu-id="47656-196">Vá tooQuick Links e, em seguida, clique em **criar um usuário**.</span><span class="sxs-lookup"><span data-stu-id="47656-196">Go tooQuick Links, and then click **Create a User**.</span></span>
   
    ![Seção Criar usuário][401]

4. <span data-ttu-id="47656-198">Em Olá **Create User** caixa de diálogo, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="47656-198">On hello **Create User** dialog, perform hello following steps:</span></span>
   
    ![Caixa de diálogo Criar usuário][402]
    
    <span data-ttu-id="47656-200">a.</span><span class="sxs-lookup"><span data-stu-id="47656-200">a.</span></span> <span data-ttu-id="47656-201">Em Olá **Email** caixa de texto, como o endereço de email do tipo saudação do usuário Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="47656-201">In hello **Email** textbox, type hello email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="47656-202">b.</span><span class="sxs-lookup"><span data-stu-id="47656-202">b.</span></span> <span data-ttu-id="47656-203">Em Olá **nome** caixa de texto Nome do tipo saudação do usuário como Britta.</span><span class="sxs-lookup"><span data-stu-id="47656-203">In hello **First Name** textbox, type hello firstname of user like Britta.</span></span>

    <span data-ttu-id="47656-204">c.</span><span class="sxs-lookup"><span data-stu-id="47656-204">c.</span></span> <span data-ttu-id="47656-205">Em Olá **Sobrenome** caixa de texto Sobrenome de saudação do tipo do usuário como Simon.</span><span class="sxs-lookup"><span data-stu-id="47656-205">In hello **Surname** textbox, type hello surname of user like Simon.</span></span>
    
    <span data-ttu-id="47656-206">d.</span><span class="sxs-lookup"><span data-stu-id="47656-206">d.</span></span> <span data-ttu-id="47656-207">Selecione **Administrador Cliente** como **Escolher Função**.</span><span class="sxs-lookup"><span data-stu-id="47656-207">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="47656-208">e.</span><span class="sxs-lookup"><span data-stu-id="47656-208">e.</span></span> <span data-ttu-id="47656-209">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="47656-209">Click **Save**.</span></span>   

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="47656-210">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="47656-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="47656-211">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooWorkrite.</span><span class="sxs-lookup"><span data-stu-id="47656-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWorkrite.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="47656-213">**tooassign Britta Simon tooWorkrite, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="47656-213">**tooassign Britta Simon tooWorkrite, perform hello following steps:**</span></span>

1. <span data-ttu-id="47656-214">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="47656-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="47656-216">Na lista de aplicativos hello, selecione **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="47656-216">In hello applications list, select **Workrite**.</span></span>

    ![link de Workrite Olá na lista de aplicativos Olá](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_app.png)  

3. <span data-ttu-id="47656-218">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="47656-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="47656-220">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="47656-220">Click **Add** button.</span></span> <span data-ttu-id="47656-221">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="47656-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="47656-223">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="47656-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="47656-224">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="47656-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="47656-225">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="47656-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="47656-226">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="47656-226">Test single sign-on</span></span>

<span data-ttu-id="47656-227">Olá o objetivo desta seção é tootest Olá a sua configuração de SSO do AD do Azure usando o painel de acesso.</span><span class="sxs-lookup"><span data-stu-id="47656-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="47656-228">Quando você clica em bloco Workrite Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour Workrite aplicativo.</span><span class="sxs-lookup"><span data-stu-id="47656-228">When you click hello Workrite tile in hello Access Panel, you should get automatically signed-on tooyour Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="47656-229">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="47656-229">Additional resources</span></span>

* [<span data-ttu-id="47656-230">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="47656-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="47656-231">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="47656-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_400.png
[401]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_401.png
[402]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_402.png

