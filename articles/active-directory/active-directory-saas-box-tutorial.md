---
title: "Tutorial: integração do Azure Active Directory com o Box | Microsoft Docs"
description: "Saiba como tooconfigure o logon único entre o Active Directory do Azure e caixa."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e13a7979761a0b30ecdaac242f1f57a7f8da54c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="c7a3b-103">Tutorial: Integração do Active Directory do Azure ao Box</span><span class="sxs-lookup"><span data-stu-id="c7a3b-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="c7a3b-104">Neste tutorial, você aprenderá como toointegrate caixa com o Azure Active Directory (AD do Azure).</span><span class="sxs-lookup"><span data-stu-id="c7a3b-104">In this tutorial, you learn how toointegrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c7a3b-105">Integrando caixa com o AD do Azure fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7a3b-105">Integrating Box with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="c7a3b-106">Você pode controlar no AD do Azure que tenha acesso tooBox</span><span class="sxs-lookup"><span data-stu-id="c7a3b-106">You can control in Azure AD who has access tooBox</span></span>
- <span data-ttu-id="c7a3b-107">Você pode habilitar seu usuários tooautomatically get conectado tooBox (logon único) com suas contas do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7a3b-107">You can enable your users tooautomatically get signed-on tooBox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c7a3b-108">Você pode gerenciar suas contas em um local central - Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c7a3b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="c7a3b-109">Se você quiser tooknow para obter mais detalhes sobre a integração de aplicativos SaaS com o AD do Azure, consulte [o que é o acesso ao aplicativo e logon único com o Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c7a3b-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c7a3b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c7a3b-110">Prerequisites</span></span>

<span data-ttu-id="c7a3b-111">tooconfigure integração do AD do Azure com caixa, você precisa Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7a3b-111">tooconfigure Azure AD integration with Box, you need hello following items:</span></span>

- <span data-ttu-id="c7a3b-112">Uma assinatura do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7a3b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c7a3b-113">Uma assinatura do Box habilitada para logon único</span><span class="sxs-lookup"><span data-stu-id="c7a3b-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c7a3b-114">Olá tootest as etapas neste tutorial, não recomendamos usar um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c7a3b-115">tootest Olá etapas deste tutorial, você deve seguir estas recomendações:</span><span class="sxs-lookup"><span data-stu-id="c7a3b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c7a3b-116">Não use o ambiente de produção, a menos que seja necessário.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c7a3b-117">Se não tiver um ambiente de avaliação do AD do Azure, você pode obter uma versão de avaliação de um mês [aqui](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c7a3b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c7a3b-118">Descrição do cenário</span><span class="sxs-lookup"><span data-stu-id="c7a3b-118">Scenario description</span></span>
<span data-ttu-id="c7a3b-119">Neste tutorial, você testará o logon único do Azure AD em um ambiente de teste.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c7a3b-120">cenário de saudação descrito neste tutorial consiste em dois elementos básicos:</span><span class="sxs-lookup"><span data-stu-id="c7a3b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c7a3b-121">Adicionar caixa de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="c7a3b-121">Adding Box from hello gallery</span></span>
2. <span data-ttu-id="c7a3b-122">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7a3b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-hello-gallery"></a><span data-ttu-id="c7a3b-123">Adicionar caixa de galeria Olá</span><span class="sxs-lookup"><span data-stu-id="c7a3b-123">Adding Box from hello gallery</span></span>
<span data-ttu-id="c7a3b-124">integração de saudação tooconfigure da caixa no AD do Azure, você precisa de tooadd caixa da lista de tooyour Olá Galeria de aplicativos SaaS gerenciados.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-124">tooconfigure hello integration of Box into Azure AD, you need tooadd Box from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="c7a3b-125">**tooadd caixa da Galeria hello, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7a3b-125">**tooadd Box from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7a3b-126">Em Olá  **[portal do Azure](https://portal.azure.com)**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c7a3b-128">Navegue muito**aplicativos empresariais**.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="c7a3b-129">Em seguida, acesse muito**todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-129">Then go too**All applications**.</span></span>

    ![Aplicativos][2]
    
3. <span data-ttu-id="c7a3b-131">Clique em **novo aplicativo** botão na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplicativos][3]

4. <span data-ttu-id="c7a3b-133">Na caixa de pesquisa hello, digite **caixa**.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-133">In hello search box, type **Box**.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="c7a3b-135">No painel de resultados de saudação, selecione **caixa**e, em seguida, clique em **adicionar** botão aplicativo hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-135">In hello results panel, select **Box**, and then click **Add** button tooadd hello application.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c7a3b-137">Configurar e testar o logon único do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7a3b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c7a3b-138">Nesta seção, você configurará e testará o logon único do Azure AD com o Box com base em um usuário de teste chamado “Brenda Fernandes”.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c7a3b-139">Para toowork de logon único, o AD do Azure precisa tooknow que usuário de contraparte Olá na caixa é tooa usuário no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Box is tooa user in Azure AD.</span></span> <span data-ttu-id="c7a3b-140">Em outras palavras, uma relação de link entre um usuário do AD do Azure e o usuário relacionado de saudação na caixa precisa toobe estabelecida.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-140">In other words, a link relationship between an Azure AD user and hello related user in Box needs toobe established.</span></span>

<span data-ttu-id="c7a3b-141">Essa relação de link é estabelecida pela atribuição de valor Olá Olá **nome de usuário** no AD do Azure como valor de saudação do hello **Username** na caixa.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Box.</span></span>

<span data-ttu-id="c7a3b-142">tooconfigure e teste de logon único do AD do Azure com caixa, você precisa Olá toocomplete blocos de construção a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7a3b-142">tooconfigure and test Azure AD single sign-on with Box, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="c7a3b-143">**[Configurando o Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse seus usuários esse recurso.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="c7a3b-144">**[Criar um usuário de teste do AD do Azure](#creating-an-azure-ad-test-user)**  -tootest AD do Azure-logon único com Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c7a3b-145">**[Criar um usuário de teste caixa](#creating-a-box-test-user)**  -toohave um equivalente do Britta Simon na caixa que é vinculado toohello AD do Azure representação do usuário.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-145">**[Creating a Box test user](#creating-a-box-test-user)** - toohave a counterpart of Britta Simon in Box that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="c7a3b-146">**[Usuário de teste de saudação do AD do Azure atribuindo](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse AD do Azure-logon único.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c7a3b-147">**[Teste o logon único](#testing-single-sign-on)**  -tooverify Olá se os trabalhos de configuração.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c7a3b-148">Configuração do logon único do Azure AD</span><span class="sxs-lookup"><span data-stu-id="c7a3b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c7a3b-149">Nesta seção, habilitar o AD do Azure-logon único no hello portal do Azure e configurar o logon único em seu aplicativo de caixa.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="c7a3b-150">**tooconfigure AD do Azure-logon único com caixa, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7a3b-150">**tooconfigure Azure AD single sign-on with Box, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7a3b-151">Em Olá portal do Azure, Olá **caixa** página de integração de aplicativos, clique em **o logon único**.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-151">In hello Azure portal, on hello **Box** application integration page, click **Single sign-on**.</span></span>

    ![Configurar Logon Único][4]

2. <span data-ttu-id="c7a3b-153">Em Olá **o logon único** caixa de diálogo, selecione **modo** como **baseado no SAML logon** tooenable-logon único.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurar Logon Único](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="c7a3b-155">Em Olá **caixa domínio e URLs** , execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7a3b-155">On hello **Box Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="c7a3b-157">Em Olá **URL de logon** caixa de texto, digite um URL usando o saudação padrão a seguir:`https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="c7a3b-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c7a3b-158">Esse valor não é real.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-158">This value is not real.</span></span> <span data-ttu-id="c7a3b-159">Atualize o valor de saudação com URL de logon real hello.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-159">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="c7a3b-160">Entre em contato com [equipe de suporte de cliente caixa](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget esse valor.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget this value.</span></span> 
 
4. <span data-ttu-id="c7a3b-161">Em Olá **o certificado de autenticação SAML** seção, clique em **Metadata XML** e, em seguida, salve o arquivo XML de saudação em seu computador.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="c7a3b-163">Clique no botão **Salvar** .</span><span class="sxs-lookup"><span data-stu-id="c7a3b-163">Click **Save** button.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c7a3b-165">tooget SSO configurado para o seu aplicativo, entre em contato com [equipe de suporte de cliente caixa](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) e fornecê-los com o arquivo de XML Olá baixado.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-165">tooget SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with hello downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="c7a3b-166">Agora você pode ler uma versão concisa dessas instruções dentro de saudação [portal do Azure](https://portal.azure.com), enquanto você estiver configurando o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="c7a3b-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="c7a3b-167">Depois de adicionar a este aplicativo de saudação **do Active Directory > aplicativos empresariais** seção, basta clicar em Olá **Single Sign-On** Olá guia e acesso inseridos documentação por meio de saudação  **Configuração** seção na parte inferior da saudação.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="c7a3b-168">Você pode ler mais sobre os recursos de documentação embedded Olá aqui: [AD do Azure inseridos documentação]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="c7a3b-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c7a3b-169">Criação de um usuário de teste do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7a3b-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="c7a3b-170">Olá objetivo desta seção é toocreate um usuário de teste no hello chamado Britta Simon de portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Criar um usuário do AD do Azure][100]

<span data-ttu-id="c7a3b-172">**toocreate um usuário de teste no AD do Azure, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7a3b-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7a3b-173">Em Olá **portal do Azure**, em Olá painel de navegação esquerdo, clique em **Active Directory do Azure** ícone.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c7a3b-175">lista de saudação toodisplay de usuários, vá muito**usuários e grupos** e clique em **todos os usuários**.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c7a3b-177">Olá tooopen **usuário** caixa de diálogo, clique em **adicionar** na parte superior de saudação da caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c7a3b-179">Em Olá **usuário** caixa de diálogo de página, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="c7a3b-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Criação de um usuário de teste do AD do Azure](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c7a3b-181">a.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-181">a.</span></span> <span data-ttu-id="c7a3b-182">Em Olá **nome** caixa de texto, tipo **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c7a3b-183">b.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-183">b.</span></span> <span data-ttu-id="c7a3b-184">Em Olá **nome de usuário** caixa de texto, Olá tipo **endereço de email** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c7a3b-185">c.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-185">c.</span></span> <span data-ttu-id="c7a3b-186">Selecione **Mostrar senha** e anote o valor Olá Olá **senha**.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="c7a3b-187">d.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-187">d.</span></span> <span data-ttu-id="c7a3b-188">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="c7a3b-189">Criação de um usuário de teste do Box</span><span class="sxs-lookup"><span data-stu-id="c7a3b-189">Creating a Box test user</span></span>

<span data-ttu-id="c7a3b-190">Nesta seção, é criado um usuário chamado Brenda Fernandes no Box.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="c7a3b-191">O Box dá suporte ao provisionamento just-in-time, que está habilitado por padrão.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="c7a3b-192">Não há itens de ação para você nesta seção.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-192">There is no action item for you in this section.</span></span> <span data-ttu-id="c7a3b-193">Se um usuário já não existe na caixa, um novo será criado quando você tenta tooaccess caixa.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-193">If a user doesn't already exist in Box, a new one is created when you attempt tooaccess Box.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="c7a3b-194">Atribuir um usuário de teste de saudação do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c7a3b-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="c7a3b-195">Nesta seção, você pode habilitar Britta Simon toouse logon único do Azure, concedendo acesso tooBox.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBox.</span></span>

![Atribuir usuário][200] 

<span data-ttu-id="c7a3b-197">**tooassign Britta Simon tooBox, execute Olá etapas a seguir:**</span><span class="sxs-lookup"><span data-stu-id="c7a3b-197">**tooassign Britta Simon tooBox, perform hello following steps:**</span></span>

1. <span data-ttu-id="c7a3b-198">No hello portal do Azure, abra a exibição dos aplicativos Olá e navegue toohello exibição de diretório e ir muito**aplicativos empresariais** , em seguida, clique em **todos os aplicativos**.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Atribuir usuário][201] 

2. <span data-ttu-id="c7a3b-200">Na lista de aplicativos hello, selecione **caixa**.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-200">In hello applications list, select **Box**.</span></span>

    ![Configurar Logon Único](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="c7a3b-202">No menu Olá Olá esquerda, clique em **usuários e grupos**.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Atribuir usuário][202] 

4. <span data-ttu-id="c7a3b-204">Clique no botão **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-204">Click **Add** button.</span></span> <span data-ttu-id="c7a3b-205">Em seguida, selecione **usuários e grupos** na **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Atribuir usuário][203]

5. <span data-ttu-id="c7a3b-207">Em **usuários e grupos** caixa de diálogo, selecione **Britta Simon** na lista de usuários de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="c7a3b-208">Clique em **selecione** botão **usuários e grupos** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c7a3b-209">Clique em **atribuir** botão **Adicionar atribuição** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c7a3b-210">Teste do logon único</span><span class="sxs-lookup"><span data-stu-id="c7a3b-210">Testing single sign-on</span></span>

<span data-ttu-id="c7a3b-211">Nesta seção, você testa a AD do Azure única configuração de logon usando o painel de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="c7a3b-212">Quando você clica em bloco caixa Olá Olá painel de acesso, você deve obter logon página tooget conectado tooyour aplicativo de caixa.</span><span class="sxs-lookup"><span data-stu-id="c7a3b-212">When you click hello Box tile in hello Access Panel, you should get login page tooget signed-on tooyour Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c7a3b-213">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="c7a3b-213">Additional resources</span></span>

* [<span data-ttu-id="c7a3b-214">Lista de tutoriais sobre como tooIntegrate aplicativos SaaS com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c7a3b-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c7a3b-215">O que é o acesso a aplicativos e logon único com o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c7a3b-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="c7a3b-216">Configurar Provisionamento de Usuário</span><span class="sxs-lookup"><span data-stu-id="c7a3b-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

