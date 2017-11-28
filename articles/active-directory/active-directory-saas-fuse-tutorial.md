---
title: "Tutorial: integração do Azure Active Directory ao Fuse | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e fusível."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5ef34f58-863a-4b37-875c-e8efa3e18bb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 720ed8af0b5de1e3bee5a40353ca0ee661766864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fuse"></a><span data-ttu-id="5883e-103">Tutorial: Integração do Active Directory do Azure ao Fuse</span><span class="sxs-lookup"><span data-stu-id="5883e-103">Tutorial: Azure Active Directory integration with Fuse</span></span>

<span data-ttu-id="5883e-104">Neste tutorial, você aprenderá como toointegrate unir com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="5883e-104">In this tutorial, you learn how toointegrate Fuse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5883e-105">Integrando fusível AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="5883e-105">Integrating Fuse with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5883e-106">Você pode controlar no AD do Azure que tenha acesso tooFuse.</span><span class="sxs-lookup"><span data-stu-id="5883e-106">You can control in Azure AD who has access tooFuse.</span></span>
- <span data-ttu-id="5883e-107">Você pode habilitar seu usuários tooautomatically get conectado tooFuse (logon único) com suas contas do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5883e-107">You can enable your users tooautomatically get signed-on tooFuse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="5883e-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5883e-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="5883e-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5883e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5883e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5883e-110">Prerequisites</span></span>

<span data-ttu-id="5883e-111">integração de tooconfigure AD do Azure com fusível, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="5883e-111">tooconfigure Azure AD integration with Fuse, you need hello following items:</span></span>

- <span data-ttu-id="5883e-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5883e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5883e-113">Uma assinatura do Fuse habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="5883e-113">A Fuse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5883e-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="5883e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5883e-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="5883e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5883e-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="5883e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5883e-117">Se não tiver um ambiente de avaliação do Azure AD, você pode [obter uma versão de avaliação de um mês](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5883e-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5883e-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="5883e-118">Scenario description</span></span>
<span data-ttu-id="5883e-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="5883e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5883e-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="5883e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5883e-121">Adicionar fusível da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5883e-121">Add Fuse from hello gallery</span></span>
2. <span data-ttu-id="5883e-122">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5883e-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-fuse-from-hello-gallery"></a><span data-ttu-id="5883e-123">Adicionar fusível da Galeria de saudação</span><span class="sxs-lookup"><span data-stu-id="5883e-123">Add Fuse from hello gallery</span></span>
<span data-ttu-id="5883e-124">integração de saudação tooconfigure do fusível no AD do Azure, você precisa tooadd fusível da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="5883e-124">tooconfigure hello integration of Fuse into Azure AD, you need tooadd Fuse from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5883e-125">**tooadd fusível da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5883e-125">**tooadd Fuse from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5883e-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="5883e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![botão de Active Directory do Azure Olá][1]

2. <span data-ttu-id="5883e-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="5883e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5883e-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5883e-129">Then go too**All applications**.</span></span>

    ![folha de aplicativos de empresa Olá][2]
    
3. <span data-ttu-id="5883e-131">tooadd novo aplicativo, clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5883e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Novo botão de aplicativo Hello][3]

4. <span data-ttu-id="5883e-133">Na caixa de pesquisa hello, digite **fusível**, selecione **fusível** no painel de resultados e clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5883e-133">In hello search box, type **Fuse**, select **Fuse** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Unir na lista de resultados de saudação](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="5883e-135">Configurar e testar logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5883e-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="5883e-136">Nesta seção, você configurará e testará o logon único do Azure AD com o Fuse, com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="5883e-136">In this section, you configure and test Azure AD single sign-on with Fuse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5883e-137">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá em fusível é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="5883e-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Fuse is tooa user in Azure AD.</span></span> <span data-ttu-id="5883e-138">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação em fusível necessidades toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="5883e-138">In other words, a link relationship between an Azure AD user and hello related user in Fuse needs toobe established.</span></span>

<span data-ttu-id="5883e-139">Fusível, atribuir valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** tooestablish relação de link de saudação.</span><span class="sxs-lookup"><span data-stu-id="5883e-139">In Fuse, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5883e-140">tooconfigure e teste de logon único do AD do Azure com fusível, é necessário Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="5883e-140">tooconfigure and test Azure AD single sign-on with Fuse, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5883e-141">**[Configurar o Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="5883e-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5883e-142">**[Criar um usuário de teste do AD do Azure](#create-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5883e-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5883e-143">**[Criar um usuário de teste fusível](#create-a-fuse-test-user)**  -toohave um equivalente do Britta Simon em fusível é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="5883e-143">**[Create a Fuse test user](#create-a-fuse-test-user)** - toohave a counterpart of Britta Simon in Fuse that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5883e-144">**[Atribuir um usuário de teste de saudação do AD do Azure](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="5883e-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5883e-145">**[Testar o logon único](#test-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="5883e-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="5883e-146">Configurar o logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5883e-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="5883e-147">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único no aplicativo fusível.</span><span class="sxs-lookup"><span data-stu-id="5883e-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Fuse application.</span></span>

<span data-ttu-id="5883e-148">**tooconfigure logon único do AD do Azure com fusível, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5883e-148">**tooconfigure Azure AD single sign-on with Fuse, perform hello following steps:**</span></span>

1. <span data-ttu-id="5883e-149">Em Olá portal do Azure, Olá **fusível** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="5883e-149">In hello Azure portal, on hello **Fuse** application integration page, click **Single sign-on**.</span></span>

    ![Link Configurar logon único][4]

2. <span data-ttu-id="5883e-151">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="5883e-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Caixa de diálogo Logon único](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_samlbase.png)

3. <span data-ttu-id="5883e-153">Em Olá **URLs e unir domínio** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5883e-153">On hello **Fuse Domain and URLs** section, perform hello following steps:</span></span>

    ![Informações de logon único de Domínio e URLs do fusível](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_url.png)
    
    <span data-ttu-id="5883e-155">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<tenant name>.fusion-universal.com/`</span><span class="sxs-lookup"><span data-stu-id="5883e-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant name>.fusion-universal.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5883e-156">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="5883e-156">This value is not real.</span></span> <span data-ttu-id="5883e-157">Atualize esse valor com hello URL de logon real.</span><span class="sxs-lookup"><span data-stu-id="5883e-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="5883e-158">Entre em contato com [equipe de suporte de cliente fusível](mailto:support@fusion-universal.com) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="5883e-158">Contact [Fuse Client support team](mailto:support@fusion-universal.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="5883e-159">Em Olá **o certificado de autenticação SAML** seção, clique em **certificado (Raw)** e, em seguida, salve o arquivo de certificado de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="5883e-159">On hello **SAML Signing Certificate** section, click **Certificate (Raw)** and then save hello certificate file on your computer.</span></span>

    ![link de download de certificado Olá](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_certificate.png) 

5. <span data-ttu-id="5883e-161">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="5883e-161">Click **Save** button.</span></span>

    ![Botão Salvar em Configurar Logon Único](./media/active-directory-saas-fuse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5883e-163">Em Olá **configuração fusível** seção, clique em **configurar fusível** tooopen **configurar o logon** janela.</span><span class="sxs-lookup"><span data-stu-id="5883e-163">On hello **Fuse Configuration** section, click **Configure Fuse** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5883e-164">Saudação de cópia **URL de logout, ID de entidade de SAML e Single Sign-On URL do serviço SAML** de saudação **seção de referência rápida.**</span><span class="sxs-lookup"><span data-stu-id="5883e-164">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuração do Fuse](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_configure.png) 

7. <span data-ttu-id="5883e-166">tooget SSO configurado para o seu aplicativo, entre em contato com [a equipe de suporte fusível](mailto:support@fusion-universal.com) e fornecê-los com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="5883e-166">tooget SSO configured for your application, contact [Fuse support team](mailto:support@fusion-universal.com) and provide them with hello following:</span></span>

    * <span data-ttu-id="5883e-167">Olá baixado **arquivo de certificado (Raw)**</span><span class="sxs-lookup"><span data-stu-id="5883e-167">hello downloaded **Certificate (Raw) file**</span></span>
    * <span data-ttu-id="5883e-168">Olá **Single Sign-On URL do serviço SAML**</span><span class="sxs-lookup"><span data-stu-id="5883e-168">hello **SAML Single Sign-On Service URL**</span></span>
    * <span data-ttu-id="5883e-169">Olá **ID de entidade de SAML**</span><span class="sxs-lookup"><span data-stu-id="5883e-169">hello **SAML Entity ID**</span></span>
    * <span data-ttu-id="5883e-170">Olá **URL de logout**</span><span class="sxs-lookup"><span data-stu-id="5883e-170">hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="5883e-171">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="5883e-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5883e-172">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="5883e-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5883e-173">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5883e-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="5883e-174">Criar um usuário de teste do Azure AD</span><span class="sxs-lookup"><span data-stu-id="5883e-174">Create an Azure AD test user</span></span>

<span data-ttu-id="5883e-175">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5883e-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Criar um usuário de teste do Azure AD][100]

<span data-ttu-id="5883e-177">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5883e-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5883e-178">No hello portal do Azure, no painel esquerdo do hello, clique em Olá **Active Directory do Azure** botão.</span><span class="sxs-lookup"><span data-stu-id="5883e-178">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![botão de Active Directory do Azure Olá](./media/active-directory-saas-fuse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="5883e-180">lista de saudação toodisplay de usuários, vá muito**usuários e grupos**e, em seguida, clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="5883e-180">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Olá "Usuários e grupos" e "Todos os usuários" links](./media/active-directory-saas-fuse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="5883e-182">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação do hello **todos os usuários** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5883e-182">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![botão Adicionar de saudação](./media/active-directory-saas-fuse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="5883e-184">Em Olá **usuário** caixa de diálogo caixa, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5883e-184">In hello **User** dialog box, perform hello following steps:</span></span>

    ![caixa de diálogo de usuário Olá](./media/active-directory-saas-fuse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="5883e-186">a.</span><span class="sxs-lookup"><span data-stu-id="5883e-186">a.</span></span> <span data-ttu-id="5883e-187">Em Olá **nome** , digite **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5883e-187">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5883e-188">b.</span><span class="sxs-lookup"><span data-stu-id="5883e-188">b.</span></span> <span data-ttu-id="5883e-189">Em Olá **nome de usuário** caixa tipo hello endereço de email do usuário Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5883e-189">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="5883e-190">c.</span><span class="sxs-lookup"><span data-stu-id="5883e-190">c.</span></span> <span data-ttu-id="5883e-191">Selecione Olá **Mostrar senha** caixa de seleção e anote o valor de saudação que é exibido no hello **senha** caixa.</span><span class="sxs-lookup"><span data-stu-id="5883e-191">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="5883e-192">d.</span><span class="sxs-lookup"><span data-stu-id="5883e-192">d.</span></span> <span data-ttu-id="5883e-193">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5883e-193">Click **Create**.</span></span>
 
### <a name="create-a-fuse-test-user"></a><span data-ttu-id="5883e-194">Criar um usuário de teste do Fuse</span><span class="sxs-lookup"><span data-stu-id="5883e-194">Create a Fuse test user</span></span>

<span data-ttu-id="5883e-195">Nesta seção, você criará uma usuária chamada Brenda Fernandes no Fuse.</span><span class="sxs-lookup"><span data-stu-id="5883e-195">In this section, you create a user called Britta Simon in Fuse.</span></span> <span data-ttu-id="5883e-196">Trabalhe com [a equipe de suporte fusível](mailto:support@fusion-universal.com) tooadd usuários de saudação na plataforma de fusível hello.</span><span class="sxs-lookup"><span data-stu-id="5883e-196">Please work with [Fuse support team](mailto:support@fusion-universal.com) tooadd hello users in hello Fuse platform.</span></span>


### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="5883e-197">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="5883e-197">Assign hello Azure AD test user</span></span>

<span data-ttu-id="5883e-198">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooFuse.</span><span class="sxs-lookup"><span data-stu-id="5883e-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFuse.</span></span>

![Atribuir função de usuário Olá][200] 

<span data-ttu-id="5883e-200">**tooassign Britta Simon tooFuse, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="5883e-200">**tooassign Britta Simon tooFuse, perform hello following steps:**</span></span>

1. <span data-ttu-id="5883e-201">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="5883e-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="5883e-203">Na lista de aplicativos hello, selecione **fusível**.</span><span class="sxs-lookup"><span data-stu-id="5883e-203">In hello applications list, select **Fuse**.</span></span>

    ![link de fusível Olá na lista de aplicativos Olá](./media/active-directory-saas-fuse-tutorial/tutorial_fuse_app.png)  

3. <span data-ttu-id="5883e-205">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="5883e-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![link de "Usuários e grupos" Hello][202]

4. <span data-ttu-id="5883e-207">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="5883e-207">Click **Add** button.</span></span> <span data-ttu-id="5883e-208">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5883e-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Painel de atribuição adicionar Olá][203]

5. <span data-ttu-id="5883e-210">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="5883e-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5883e-211">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5883e-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5883e-212">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="5883e-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="5883e-213">Testar logon único</span><span class="sxs-lookup"><span data-stu-id="5883e-213">Test single sign-on</span></span>

<span data-ttu-id="5883e-214">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="5883e-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5883e-215">Quando você clica em bloco fusível Olá Olá painel de acesso, você deve obter automaticamente assinado em tooyour fusível do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5883e-215">When you click hello Fuse tile in hello Access Panel, you should get automatically signed-on tooyour Fuse application.</span></span>
<span data-ttu-id="5883e-216">Para obter mais informações sobre o painel de acesso, consulte [toohello Introdução painel de acesso](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5883e-216">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5883e-217">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="5883e-217">Additional resources</span></span>

* [<span data-ttu-id="5883e-218">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="5883e-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5883e-219">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5883e-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fuse-tutorial/tutorial_general_203.png

